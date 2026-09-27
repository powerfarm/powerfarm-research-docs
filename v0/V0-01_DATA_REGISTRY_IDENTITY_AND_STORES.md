# V0-01 — Data: Registry, Identity, Content Store, Minivault and Operational Stores

**Status:** WORKING V0, adopted
**Canon:** PF-03 §§3.2–3.8, 3.12–3.13; PF-04 §1.4

Target for Powerfarm data: where each kind of state lives, who owns it, how things come into existence, and how authority is computed.
- Names: [V0-07](V0-07_NAMES_AND_ADDRESSES.md).
- Rebuild: [V0-03](V0-03_REBUILD.md).
- Delta and plan: [V0-00](V0-00_DELTA_AND_PLAN.md).

---

## 0. Principles

1. **Institutional and operational state live in different databases.** What Powerfarm *recognizes* (who exists, which contracts are current, who may do what) lives in the Identity substrate. What agents *observe* (signals, inventories, conversations) lives in the Antenna observation store.
2. **Entities are governed by contracts.** No entity gives itself a type. Types are established by contracts, so the contracts table exists before any entity.
3. **Everything has a name:** entities, objects and contracts, including every type. Exact bytes have a digest.
4. **Nothing is silently erased.** Contracts change by new generation, and earlier generations stay. Entities, objects and contracts are retired. Stored bytes are never overwritten.
5. **Authority is computed at request time from current contracts.** Holding a login grants nothing. When a contract generation changes, everyone it covers gains or loses the corresponding authority immediately. Nowhere is a copy of permissions kept.
6. **There is one list of people and agents: the entities.** Logins and machine credentials are *bindings* (keys) to entities, never a second list.
7. **One fingerprint: SHA-256.** Exact bytes, contract documents and Minivault revisions are all named by the SHA-256 of their bytes. A digest identifies content. It is not a capability.
8. **All writes enter through the institutional API.** Nothing writes to tables directly. **The migration creates only empty tables and rules, never rows.** The first write is the **Foundation Act**, performed once through the API.
9. **Copies are projections.** Every replica, cache or search projection can be rebuilt from its source and never becomes authority.
10. **Everything institutional is rebuildable** (PF-03 §3.3). Every write is an act, recorded in order in the act log (§6.1). Replaying the acts over the preserved content rebuilds the Registry, the Content Store catalog and Minivault's recognitions (V0-03).

---

## 1. Map

```text
┌────────────── Identity substrate: powerfarm.app/store/company ───────────────┐
│  (Supabase project powerfarm.kernal, ref ekjlmclhqnsstfjzuabz, eu-west-1)    │
│                                                                              │
│  Registry        entities, objects, versions, contracts (by generation)      │
│  Identity        OAuth 2.1 server, bindings (keys → entities), admissions,   │
│                  acceptances                                                 │
│  Content Store   exact bytes by SHA-256 + manifests (private Storage bucket) │
│  Minivault       promoted meaning over the same Content Store                │
│  Act log         every act, in order, hash-chained: the story (V0-03)        │
│  API             the only door in and out (api.powerfarm.app)                │
└───────────────┬───────────────────────────────────────────▲──────────────────┘
                │ read-only Registry replica                │ login + "may I?"
                ▼                                           │
┌─────────── Antenna observation store ────────────┐  ┌─────┴──────────────────┐
│  powerfarm.app/store/antenna                     │◀─│ Coloured Places        │
│  signals, inventories, agent events              │  │ places.powerfarm.app   │
│  read-only Registry replica                      │  │ (projection)           │
└───────────────▲──────────────────────────────────┘  └────────────────────────┘
                │ each agent writes only its own observations
     powerfarm.app/agent/lab-8gb · powerfarm.app/agent/lab-512
     (powerfarm.app/agent/lab-256: never required)
```

Outside these databases (§9): GitHub, Google Drive, CloudKit (per V0-02) and the LABs' local agent state.

**Why two databases.** Operational state belongs to the software that produces it (PF-03 §3.3), and observational evidence, including heartbeat and signals, is Antenna's responsibility (PF-03 §§3.9, 3.13). The observation store is therefore declared as Antenna's store under a store-authority contract. It is not a new architectural organ. Coloured Places is a projection over both databases (PF-03 §3.12).

---

## 2. Registry

### 2.1 The four basics

The Registry keeps the four basics of Registry Core v0. Tables may carry supporting columns, but no new basic is added. Every write to these tables also appends one act to the act log (§6.1).

| table | meaning | main columns |
|---|---|---|
| entities | things that act | name, **type**, title, summary, created at/by, retired at, reason |
| objects | things that are acted on | name, **type**, title, summary, created at/by, retired at |
| versions | exact bytes of an object | object, version, content (digest or manifest digest), source (repository, revision, path), recognized at/by, superseded at/by, retired at |
| contracts | recognized definitions and relationships, by generation | name, generation, **type**, subject, provider, consumer, holds, document digest, effective from/until, recognized at/by, acceptance receipt digest, superseded at/by, retired at |

**Entities act; objects are acted on.** An entity holds keys, signs in and is the one whose authority is computed. An object never acts: it is owned, placed, versioned and referred to. Entities and objects share one space of names.

Permissions, offices, placements and store authority are all **contracts**. The Registry has no other kind of record.

### 2.2 Types come from contracts

**Every type column points to a current contract:**
- contract.type → a Contract Type;
- entity.type → an Entity Type;
- object.type → an Object Type;
- every action → an Action Type.

These four are the **type roots**: the only contract types the Registry knows by name. The first contract of the Foundation Act, *Contract Type*, is its own type. Every other type, including every other contract type, is recognized through the API, one contract at a time, with no deploy.

A type exists only while a contract defining it is current.

A Contract Type document states which **participants** its contracts name. Definitions (types, offices) name none: a definition exists before anything it defines. Relationships name at least a subject, and a provider and consumer where the relationship has those roles. Participants are entities or objects.

### 2.3 Birth order

| phase | what is recognized | table |
|---|---|---|
| **A. First two contracts of the Foundation Act** | 1. *Contract Type* (type: itself) · 2. *Entity Type* (type: Contract Type) | contracts |
| **B. Contract types** | *Object Type*, *Action Type*, then the contract types V0 uses (below) | contracts |
| **C. Enumerations** | entity types · object types · action types (below) | contracts |
| **D. Things** | entities and objects, each referencing the contract of its type; then the contracts between them | entities, objects, contracts |

The birth order is the first chapter of the story (V0-03). Every later act follows it in the act log.

**V0 contract types** (recognized in the story; the Registry knows none of them by name):

| contract type | a contract of this type… | participants |
|---|---|---|
| office | defines a seat: who may hold it and the powers it gives its holders | none |
| mandate | puts one holder in one office for an effective interval | subject: the holder; holds: the office |
| permission | gives powers to its subject | subject |
| app-contract | admits an app (V0-02) | subject: the app |
| engine-capability | declares what an engine provides (V0-02) | subject: the engine |
| store-authority | declares a store's owner and what it is authoritative for | subject: the store; provider: the owner |
| search-contract | declares a Search source or projection (V0-06) | subject |
| machine-placement | places an agent, Host Runner, app or engine on a machine | subject: the placed entity; provider: the machine |
| secret-consumer | lets an entity use a secret reference (§2.10) | subject: the consumer; provider: the secret |
| execution-approval | approves one exact plan or effect by digest (§2.7) | subject |
| backup-custody | declares a copy and its custodian (§9) | subject |

**V0 entity types** (names follow V0-07):

| type | name form | examples |
|---|---|---|
| person | `powerfarm.app/person/*` | the Director's holder |
| agent | `powerfarm.app/agent/*` | LLM occupants: the local agents (`powerfarm.app/agent/lab-8gb`), and LLM sessions acting through a bound credential |
| app | `powerfarm.app/app/*` | `powerfarm.app/app/coloured-places`, `powerfarm.app/app/minivault-web` |
| service | `powerfarm.app/service/<service>` | `powerfarm.app/service/antenna`, `powerfarm.app/service/heartime`, `powerfarm.app/service/search` |
| host-runner | `powerfarm.app/host-runner/*` | `powerfarm.app/host-runner/lab-8gb` |
| engine | `powerfarm.app/engine/*` | `powerfarm.app/engine/google-adk` |
| mcp | `powerfarm.app/mcp/*` | MCP servers admitted by contract |

**V0 object types:**

| type | name form | examples |
|---|---|---|
| sector | `powerfarm.app/sector/<sector>` | `powerfarm.app/sector/identity`, `powerfarm.app/sector/continuity`, `powerfarm.app/sector/research` |
| machine | `powerfarm.app/machine/*` | `powerfarm.app/machine/lab-8gb`, `powerfarm.app/machine/lab-512` |
| process | `powerfarm.app/process/*` | `powerfarm.app/process/manhattan` |
| store | `powerfarm.app/store/*` | `powerfarm.app/store/company`, `powerfarm.app/store/antenna` |
| repository | `powerfarm.app/repository/*` | Powerfarm-native repositories |
| secret | `powerfarm.app/secret/*` | secret references (§2.10) |
| search-source | `powerfarm.app/search-source/*` | per V0-06 |
| projection | `powerfarm.app/projection/*` | Search projections (V0-06) |

and, **with versions**:
- institutional: document, software, schema, dataset, prompt, capability, execution-bundle, migration-evidence;
- Minivault kinds (§5): program, component, knowledge, idea, decision, trajectory, unknown.

**V0 action types:** view, converse, propose, publish, release, approve, admit-person, recognize-contract, inscribe, grant, store-content, read-content, write-observation.

Each Action Type contract names exactly one **authority** from the institutional vocabulary (OBSERVE · JUDGE · PROPOSE · GENERATE · EXECUTE · ORCHESTRATE · PERSIST · AUTHORIZE), so types, offices and permissions speak one language:

| action types | authority |
|---|---|
| view, read-content | OBSERVE |
| converse, propose | PROPOSE |
| write-observation, store-content, inscribe, publish | PERSIST |
| approve, release, admit-person, recognize-contract, grant | AUTHORIZE |

### 2.4 Machine-readable contract documents

Each contract generation points to exactly one document: JSON bytes in the Content Store. The Registry verifies the digest before recognizing the generation. The human-readable text and the executable terms live in the same document.

- A **Contract Type** document carries the JSON Schema that documents of that type must satisfy, and the participants its contracts name.
- An **Entity Type** document declares:
  - the name pattern;
  - **rights** (what every entity of the type may do);
  - **duties** (what it must do).
- An **Object Type** document declares the name pattern and whether objects of the type have **versions**. For those that do, it carries the JSON Schema their content must satisfy and names the kernel validator that checks what a schema alone cannot. Minivault kinds are object types with versions (§5), so adding a kind is recognizing one contract.
- An **Action Type** document names its authority.
- Any other contract's document carries its own terms. The Registry reads two of them: **powers** (what may be done, on what) and **holders** (the entity types that may hold the contract).

Example: the Entity Type document for *agent*.

```json
{
  "name": "Agent",
  "text": "An agent is a program that observes and acts for Powerfarm at a declared place.",
  "ids": "powerfarm.app/agent/*",
  "rights": [{ "may": "write-observation", "resource": "self" }],
  "duties": [
    { "must": "send-signals", "every": "PT1M" },
    { "must": "send-inventory", "every": "PT15M" }
  ]
}
```

### 2.5 Computing authority

```text
may(entity, action, resource) =
    rights of the entity's type                         (its current Entity Type contract)
  + powers of current contracts that name it as subject (a permission)
  + powers of current contracts it holds                (through a current contract that names it
                                                         as subject and holds that contract, when
                                                         the held contract accepts its type as holder)
```

- A contract that declares **holders** gives its powers only to those who hold it. Any other contract gives its powers to its subject.
- The answer is `true`, `false` or `unknown`. Only `true` passes; `unknown` carries its reason.
- An agent acting for a person never exceeds that person: the effective rights are the intersection of both.
- **Authority never widens:** recognizing a contract that gives powers requires *grant* for its subject, and the one recognizing it must hold every power it gives.

For an office governed by an autonomy matrix (§2.8), what a mandate lets its holder do *without asking* is capped by the rung of each operation class.

Duties are queryable in the same way. The Antenna store compares them with observed facts (§7.3).

### 2.6 Acceptance

Persons accept their Entity Type contract and their mandates. Each acceptance receipt is stored in the Content Store.

- A new generation that only adds rights takes effect without new acceptance.
- A new generation that adds duties requires acceptance again. Until then, the person holds no authority under it.
- The machine decides which case applies by comparing the two generations.

### 2.7 Approval

Consequential effects require explicit authorization under the governing contract. They include destructive machine change, giving powers, and adoption of a registry target.

Where practical, an approval binds to the exact immutable plan or effect by digest. A materially changed plan requires a new approval.

A Minivault publication that changes an item's effects needs this approval before it is recognized (§5).

### 2.8 Offices and the autonomy matrix

An **office** is a contract whose powers go to whoever holds it. A **mandate** is a contract whose subject is the holder and which holds the office, for an effective interval. By convention a mandate is named after both: `powerfarm.app/contract/mandate.<office>.<holder>`.

V0 has two offices:

| office | held by | meaning |
|---|---|---|
| `powerfarm.app/contract/director` | a person (the owner) | decides, adopts contracts, approves effects |
| `powerfarm.app/contract/engineer` | agents (LLM occupants) | builds, observes, diagnoses, proposes; gains autonomy with time and knowledge |

The Engineer office's document carries, in machine-readable terms, the **autonomy matrix**: for each **operation class**, the rung at which engineers may act.

| rung | meaning |
|---|---|
| OBSERVE | inspect, diagnose, propose, verify; nothing changes |
| SUGGEST | propose one specific declared operation; the Director accepts or rejects each time |
| SAFE-AUTO | resolve, apply, retry and verify within an allowlist of reversible operations; exceptions surface |
| POLICY-AUTO | operate routinely within policy; only a material delta, a boundary or a novel situation surfaces |

**Laws of the matrix:**

1. **Per class, never global.** "Engineer autonomy = 3" means nothing. Each operation class earns its rung separately.
2. **Earned by precedent.** A class rises only when the record supports a statement of the form: *"for operation X, with input in band Y, there were N approvals and zero denials, under agent version Z, whose evaluation passes."* Before that, a rung is opinion.
3. **Precedent is indexed by input, not by operation type.** A young institution sees only small cases; a matrix keyed by operation type learns "this is safe" and then auto-resolves the first large case. Recorded decisions therefore keep the relevant input dimensions.
4. **Regressible.** A rung is lost when the evidence that earned it ages out, when risk changes, or when rollback stops being demonstrably reliable. Descent is normal operation, not an incident.
5. **Authority survives autonomy.** Autonomy governs how much a proven mechanism may do without asking; it never removes the need for authority. Protected destructive operations and external effects keep a human gate at every rung.
6. **Evidence is never authored by its subject.** An engineer cannot produce the evidence that promotes it. A rise is a new generation of the Engineer office, recognized by the Director; a regression may be computed automatically.
7. **The matrix is a resolver, not a rewrite.** It plugs into the runtime's existing approval seam (the agent asks, the resolver answers from the matrix or routes to the Director). Deterministic hand-written rules may exist before any learned rung; evaluations detect when a rung starts deciding wrongly.

**Two edges carry this:**
- **Authority descends:** mandate → permission → run → effect, and never widens.
- **Evidence ascends:** act → receipt → evidence → promotion, and is never authored by its subject.

**The precedent ledger already exists.** The agents' runtime durably records its events, including requests for actions, approval requests and decisions, and results. Every one of these events is copied to the Antenna store with the tool input, the deciding principal and the agent version. The matrix reads that ledger; nothing new has to be invented to feed it.

In V0 every operation class starts at OBSERVE or SUGGEST.

Example (terms of the Engineer office):

```json
{
  "name": "Engineer",
  "holders": ["agent"],
  "matrix": [
    { "class": "observe-lab",           "rung": "OBSERVE" },
    { "class": "restart-own-agent",     "rung": "SUGGEST" },
    { "class": "prune-rebuildables",    "rung": "SUGGEST", "reversible": true },
    { "class": "delete-anything",       "rung": "SUGGEST", "protected": true },
    { "class": "change-tunnel",         "rung": "SUGGEST", "protected": true }
  ],
  "evidence_expires_after": "P90D"
}
```

### 2.9 Names

Names follow **V0-07 (Names and Addresses)**:
- things are `powerfarm.app/<type>/<name>`;
- contracts are `powerfarm.app/contract/<name>`;
- services are `<service>.powerfarm.app`;
- exact bytes are `sha256:<hex>`.

The name is the identity, the address and the link.

- Names identify institutional things, never provider objects, filesystem paths or database rows. A name says *what*, never *where*.
- Provider identities (Supabase user, Apple, GitHub, machine credential, OAuth subject) are **bindings** to names. Replacing a provider must not rename the institutional thing.
- Names are short, stable, lowercase and in English, and they are never reused. Titles and texts may be in Portuguese.

### 2.10 Secrets

The Registry stores **secret references**, never values. A reference is an object of type *secret*. A *secret-consumer* contract declares who may use it. A reference records:
- owner;
- provider or system;
- allowed consumers;
- storage location reference;
- rotation policy;
- revocation path;
- last verification date;
- state (active, rotating, revoked).

Live secret values must never enter:
- Git;
- Registry rows;
- Search or any other projection;
- receipts;
- the Content Store.

Rotation precedes deletion when exposure is possible.

A rebuild never restores secret values: it issues new ones, in the order recorded in V0-03, and binds them to the same references.

---

## 3. Identity: authentication as a keyring

- **The list of people is the Registry.** The Supabase Auth user table is a keyring: each account is a key, and **every key must be bound to exactly one person entity**.
- **Contact data stays in Identity, never in the Registry.** This includes e-mail.

| table | meaning |
|---|---|
| bindings | login account → person entity (one account per person in V0) |
| admissions | invited e-mail → intended person entity, admitted by, validity, used at |
| acceptances | who accepted which generation of which contract, and when (receipt digest) |

**Sign-in** is passwordless: an e-mail link or a passkey, at `id.powerfarm.app`. The passkey relying-party ID is `powerfarm.app`, so one passkey works for every Powerfarm service (V0-07 §3).

**Gates** (Supabase Auth hooks, implemented as Postgres functions; the HTTP form has a known error-format bug):

| situation | result |
|---|---|
| sign-up without an admission | refused before the account exists |
| person without a current Entity Type contract, or with an overdue acceptance | no new access token is issued, and the API denies everything |
| person entity retired | account blocked, open sessions revoked |
| login account deleted | the person remains in the Registry with its history, without a key until re-admitted |

**OAuth 2.1:** the Identity substrate is the authorization server for everything.
- Each **app** is an entity of type *app*. Its OAuth clients are keys bound to that entity.
- **ChatGPT and Claude** connect through MCP with OAuth, always on behalf of a person, and never with more authority than that person.
  - **Status as of 2026-09-26:**
    - the Supabase OAuth 2.1 server is beta;
    - open bug `supabase/auth#2820` blocks MCP connectors that use public clients, `offline_access` or the `resource` parameter;
    - tokens are not audience-bound (RFC 8707 is ignored), which MCP 2026-07-28 requires;
    - only Dynamic Client Registration is offered, not Client ID Metadata Documents.
  - The MCP door therefore stays **closed** until this is fixed or an OAuth bridge in front of Identity is adopted. Human sign-in is unaffected.
- Each **agent** has its own machine credential, bound to its agent entity.

---

## 4. Content Store

- **Content:** exact bytes, named `sha256:<hex>`. Content never changes and is never overwritten.
- **Content table:** digest, size, media type, stored at, stored by (entity).
- **Manifest:** JSON listing other content (`{path, digest, size}`). Compound values (software trees, evidence sets, releases) are manifests. The Registry recognizes the manifest.
- **Storing:** the caller sends bytes, and the API computes the digest and records the content only if it matches.
- **Reading:** a digest is not a capability. Reads go through the API, which asks the Registry whether the caller may read that content, through the version, contract or act that references it, or because it is public.
- **Storing is not recognizing.** Content means nothing institutionally until the Registry recognizes it as a version or a contract document.
- **Where:** a private Supabase Storage bucket owned by `powerfarm.app/store/company`. The key of stored content is its digest.
- **Integrity:**
  - the bucket's access rules allow **insert only**: no update, no delete, so nothing is overwritten;
  - Supabase does not verify content digests, so the API computes SHA-256 server-side before recording content;
  - a periodic sweep re-hashes stored content and reports any mismatch.

**Custody:**
- promoted immutable bytes must be addressable and independently verifiable;
- material company bytes need off-machine custody;
- backup policy stays independent of synchronization;
- a redundancy claim requires a distinct failure domain.

The copies that satisfy these rules are listed in §9.

---

## 5. Minivault

Minivault preserves what promoted things **mean** (PF-03 §3.5): typed, immutable revisions of meaning (programs, components, knowledge, decisions, open questions), with provenance and relations. The Registry decides who exists and who may act; Minivault never keeps its own people or permissions.

### 5.1 Items, kinds and revisions

- **An item is an object with versions.** Its name is `powerfarm.app/<kind>/<name>`, for example `powerfarm.app/program/intake.review` (V0-07).
- **A kind is an object type.** Each kind is an Object Type contract whose document holds the kind's JSON Schema and names the kernel validator (§2.4). Adding a kind is recognizing one contract; no deploy.
- **A revision is canonical bytes.** The kernel canonicalizes the item's value (RFC 8785) and stores the bytes in the Content Store. The revision's id is the `sha256:` of those bytes, the same fingerprint as every other object (§0, principle 7).
- **Identity and authority are not kinds.** People, agents and their permissions live in the Registry. A Minivault item refers to them by name.
- **The `unknown` kind** records an open question as an item: the question, why it matters, the evidence that would answer it, and its resolution. Not knowing is an answer Powerfarm records.

### 5.2 Publication is recognition

| Minivault act | What happens in the Registry |
|---|---|
| publish | a new version is recognized and the current one is superseded; the database guarantees one current version, and the publish carries the version it expects to replace |
| undo (revert) | the earlier bytes are **published again as a new version**, naming the version they restore and the reason; history only moves forward |
| deprecate | a reversible flag on the item; the item stays readable |
| retire | the object is retired in the Registry; final |
| release | anyone may read that version (`release`, AUTHORIZE) |

### 5.3 Who may do what

Minivault asks the Registry `may(entity, action, resource)` for every operation. The answer is `true`, `false` or `unknown`; only `true` passes, and `unknown` carries its reason.

| operation | action type |
|---|---|
| read an item or revision | read-content |
| draft, propose a revision | propose |
| publish | publish; plus an approval (§2.7) when the change alters the item's effects |
| review a proposal | approve |
| make a version public | release |
| change who may act on an item | grant |

An agent acting for a person never exceeds that person: its effective rights are the intersection of both. An agent's own permissions are its scope.

When an engineer must ask before publishing is decided by the Engineer autonomy matrix (§2.8).

### 5.4 What stays inside Minivault

Drafts, proposals and reviews, relations between revisions, derivations and subscriptions are Minivault's operational state. Storing is not recognizing: none of it is institutional until a publication is recognized.

### 5.5 Where it runs

- The kernel (canonicalization, validation, operations, diff, explanation, lint, composition, search ranking) is a TypeScript package in `powerfarm/minivault`. On Supabase it runs in Edge Functions (§12).
- `powerfarm.app/app/minivault-web`, at `vault.powerfarm.app`, is the human and LLM interface over Minivault: a projection, never a second authority.

---

## 6. Institutional API

The API is the only door, at `api.powerfarm.app`. Every call follows the same path: **key → entity → may? → act → record the act.**

| operation | who may (after the Foundation Act) |
|---|---|
| Foundation Act | nobody: it runs once on an empty Registry and then closes forever |
| recognize a contract or a new generation | holders of *recognize-contract* |
| retire a contract, entity or object | the same |
| inscribe an entity or an object | holders of *inscribe* for its name |
| admit a person | holders of *admit-person* |
| accept a contract | the person concerned |
| give powers (a permission or a mandate), or retire them | holders of *grant*, who hold those powers themselves |
| store and read content | per contract |
| propose, publish, release in Minivault | per §5.3 |
| "who am I" and "may I?" | any valid key |

**Foundation Act.** It recognizes the minimum needed for someone to hold authority:
- phases A and B;
- the contract types *office* and *mandate*;
- the entity type *person*;
- the Director's action types;
- the office `powerfarm.app/contract/director`;
- the first person;
- that person's Director mandate;
- that person's admission.

The first person's name and login e-mail are chosen at Foundation and are not recorded in this public document. Everything else (agents, machines, apps, stores, other people, further types) is inscribed afterwards through the API. The Foundation Act is act number 1 in the act log.

### 6.1 The act log

Every successful write through the API appends one act:

| field | meaning |
|---|---|
| sequence | strictly increasing number; the act's name is `powerfarm.app/act/<sequence>` |
| at | time of the act |
| actor | the entity that acted, and the person it acted for, if any |
| action | the action type |
| target | the name of the thing acted on |
| content | the SHA-256 of the act's payload: the terms of the operation, kept in the Content Store |
| previous | the hash of the previous act |
| hash | this act's hash, over a fixed encoding of the fields above, computed by the database |

The act log is three things at once:
- **the audit:** who did what, when, and under which authority;
- **the event stream:** workers and notifications read it;
- **the story:** replayed in order over the preserved content, it rebuilds the institution (V0-03).

Acts are never edited or removed. A correction is a new act.

---

## 7. Operational: Antenna observation store

`powerfarm.app/store/antenna` is a Neon Postgres database created through the Vercel integration. It is declared by a store-authority contract with `powerfarm.app/service/antenna` as owner.

**Cost (researched 2026-09-26):**
- Launch plan: US$0.106 per CU-hour. An always-on 0.25 CU compute costs about US$19/month, plus US$0.35 per GB-month of storage.
- The free plan cannot stay awake for per-minute writes: it scales to zero after 5 minutes and includes 100 CU-hours per month.

### 7.1 Tables

| table | contents | retention |
|---|---|---|
| agents | each writing agent (id = agent entity) and the SHA-256 of its credential | permanent |
| current signals / signal history | disk, memory, tunnels, Manhattan, cloud endpoints… every minute | 14 days of history |
| inventories | what exists on each LAB; **written only when something changes**, otherwise a "still identical at T" mark | 14 days (the latest always kept) |
| events | copies of agent conversation events | 180 days |

Each agent has its own database role, and that role can write only its own machine's observations.

### 7.2 Registry projection

- A read-only projection of types, entities, objects and current contracts with their documents. The principal agent refreshes it through the Registry API; the reserve takes over if the principal is silent.
- V0 does **not** use database-to-database logical replication. It would require Supabase's IPv4 add-on, an allowlist of Neon's egress addresses and replication slots, and it does not carry schema changes.
- The projection never writes back and can be rebuilt from scratch at any time.

### 7.3 Views enabled by the projection

- **Existence × recognition.** The four states:
  - recognized;
  - recognized but absent;
  - present but not recognized;
  - present and must not exist.
- **Duties × facts.** For example, "agents must send signals every minute" compared against received signals. Entities in breach of a duty are listed.

### 7.4 Access

- **Agents** write only their own observations.
- **Coloured Places** reads, but only after the Registry confirms that the signed-in person may view.
- No other access.

**Census note.** PF-03 §3.13 separates due-ness (Heartime), probing (Continuity) and recording (Antenna). In V0, each agent's fixed schedule stands in for Heartime-issued census obligations. The recorded evidence and its owner are unchanged when Heartime takes over.

### 7.5 Heartbeats and the external observer

- **Signals and inventories are produced by deterministic code** in each agent's runtime. A model is never woken to produce them; it wakes only to converse or judge.
- **The external observer** lives in the Identity substrate, a different failure domain from the LABs:
  - each agent sends one small "alive" mark to the API every 15 minutes;
  - a scheduled job compares each agent with its duty;
  - it e-mails the Director **only when an agent's state changes** (alive → silent, silent → alive), never on every check;
  - once a week it e-mails that it is still watching, so its own silence is visible.
- One last-seen time per agent is the only observation kept in the Identity substrate. The alive marks also keep the substrate active on the provider's free plan.

---

## 8. Agents and Host Runners

- **Agents** (`powerfarm.app/agent/*`) observe, converse and propose. They may hold the Engineer office.
- **Host Runners** (`powerfarm.app/host-runner/*`) remain the deterministic, allow-listed effect boundary of V0-02, and never treat LLM output as approval.
- An agent and the Host Runner on the same LAB are different entities.
- **LAB 256** is outside the expected ecosystem population (V0-02). An agent may run there, but nothing may depend on it.

---

## 9. Outside the databases

| place | holds | authority? |
|---|---|---|
| GitHub | source, canon, contract drafts | none for contracts: a text counts only after it is stored in the Content Store and recognized. Until `powerfarm.app/document/*` versions are recognized, the Director's merge adopts canon; from then on recognition adopts it, and GitHub is a projection |
| Google Drive "Powerfarm Backup" | cold archive of the LABs' organized folders; snapshots of the Content Store and of the act log | none; items may be promoted and recognized |
| CloudKit | contract-provisioned app and engine databases (V0-02) | owned by the declaring app or engine |
| LABs | agent queues and credentials; LAB 8GB also holds the copy of the Content Store and the act log | none; rebuildable, except credentials |
| Vercel | Coloured Places (no own state), AI Gateway | none |

**Copies:**

| what | copy | check |
|---|---|---|
| act log | exported nightly and pulled by LAB 8GB | the hash chain verifies |
| Content Store bytes | full copy on LAB 8GB, refreshed at least monthly; snapshots in Google Drive; a third copy on Cloudflare R2 if its cost stays negligible | all content re-hashed against its name |
| Identity substrate database | the provider's own backups | restore tested in the rebuild drill (V0-03) |
| Antenna store | point-in-time restore | operational: restored, or its loss declared |

The act log and the Content Store are enough to rebuild everything institutional (V0-03).

---

## 10. Admission law

A thing belongs in the Registry only when it has an institutional purpose expressible as:
- identity;
- recognized version;
- contract;
- contract giving powers;
- declared store and owner;
- placement or capability;
- Search source or projection;
- a documented temporary exception.

Everything else may exist in the world without being part of Powerfarm.

The Registry must answer mechanically:
- what exists, and which version is recognized;
- who owns it, and which contract governs it;
- where an admitted app or engine is placed;
- which store it owns, and what that store is authoritative for;
- which contracts permit protected actions;
- which secret reference a consumer requires;
- how it is onboarded, verified, retired and recovered;
- where promoted content can be resolved and verified;
- which Search sources expose it.

No authority may be inferred from physical presence, provider accounts or connectivity.

---

## 11. Kept references

**The book** (Supabase project `vbgzdqdlarulpfsyjrke`, "Google ADK mapping") is an acquired reference work:
- it is kept, and its existence is not Powerfarm's to decide;
- it is read, never used as a backend;
- no DDL is run on it;
- it may be recognized as a Research reference.

---

## 12. On Supabase

Where each part lives on the current provider. Every surface has a portable equivalent: any Postgres, any S3-compatible storage, any OIDC provider, any JavaScript runtime.

| part | Supabase surface |
|---|---|
| Registry, Identity tables, Content Store catalog, act log, Minivault | Postgres schemas `registry`, `identity`, `content`, `acts`, `vault` |
| access to those tables | none directly: every table denies everything; the API's functions check `may()` and write the act |
| the API | Postgres functions, plus Edge Functions for the Minivault kernel and uploads, at `api.powerfarm.app` |
| sign-in and gates | Supabase Auth: passwordless; Before User Created hook (admission); Custom Access Token hook (current contract) |
| apps signing in with Powerfarm | the OAuth 2.1 server |
| Content Store bytes | a private Storage bucket, insert only; the key is the digest |
| integrity sweep, external observer | scheduled jobs (`pg_cron`, with `pg_net` for e-mail) |
| later | queues for workers (`pgmq`), Realtime notifications, the MCP door |

**Limits of the free plan:** 1 GB of Storage, 500 MB of database, and a pause after seven quiet days. The external observer's alive marks keep the project active.
