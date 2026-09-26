# V0-01 — Data: Registry, Identity, Content Store, Minivault and Operational Stores

**Status:** WORKING V0, proposed for Director adoption
**Date:** 26 September 2026
**Canon:** PF-03 §§3.2–3.8, 3.12–3.13; PF-04 §1.4; `powerfarm-specs/specs/REGISTRY_CORE_v0.md`

**Replaces:**
- the previous V0-01 (Identity, Registry and Minivault);
- V0-03 (Namespace, Authority and Secrets);
- V0-05 (Ideal Registry V0).

**Retires:** V0-04 (Current Registry Situation). Its history remains in Git.

This is the single V0 materialization plan for Powerfarm data: where each kind of state lives, who owns it, how things come into existence, and how authority is computed. PF-03 remains the architecture. This document chooses the current materialization, and those choices are replaceable.

---

## 0. Principles

1. **Institutional and operational state live in different databases.** What Powerfarm *recognizes* (who exists, which contracts are current, who may do what) lives in the Identity substrate. What agents *observe* (signals, inventories, conversations) lives in the Antenna observation store.
2. **Entities are governed by contracts.** No entity gives itself a type. Types are established by contracts, so the contracts table exists before any entity.
3. **Everything has an id:** types, contracts, entities, offices, mandates, secret references, stores and objects.
4. **Nothing is silently erased.** Contracts change by new generation, and earlier generations stay. Entities are retired. Grants are revoked. Stored bytes are never overwritten.
5. **Authority is computed at request time from current contracts.** Holding a login grants nothing. When a contract generation changes, everyone it covers gains or loses the corresponding authority immediately. Nowhere is a copy of permissions kept.
6. **There is one list of people and agents: the entities.** Logins and machine credentials are *bindings* (keys) to entities, never a second list.
7. **Exact bytes are content-addressed (SHA-256).** A digest identifies content. It is not a capability.
8. **All writes enter through the institutional API.** Nothing writes to tables directly. **The migration creates only empty tables and rules, never rows.** The first write is the **Foundation Act**, performed once through the API.
9. **Copies are projections.** Every replica, cache or search projection can be rebuilt from its source and never becomes authority.

---

## 1. Map

```text
┌──────────────── Identity substrate: pf.store.supabase.company ────────────────┐
│  (Supabase project powerfarm.kernal, ref ekjlmclhqnsstfjzuabz, eu-west-1)     │
│                                                                              │
│  Registry        types, contracts (generations), entities, artifacts, grants │
│  Identity        OAuth 2.1 server, bindings (keys → entities), admissions,   │
│                  acceptances                                                  │
│  Content Store   exact bytes by SHA-256 + manifests (private Storage bucket) │
│  Minivault       promoted semantic objects over the same Content Store       │
│  API             the only door in and out                                    │
└───────────────┬───────────────────────────────────────────▲─────────────────┘
                │ read-only Registry replica                 │ login + "may I?"
                ▼                                            │
┌──── Antenna observation store: pf.store.neon.antenna ───┐  ┌──────┴───────────────┐
│  signals, inventories, agent conversation events        │◀─│ pf.app.coloured-places│
│  read-only Registry replica                              │  │ (projection, Vercel)  │
└───────────────▲──────────────────────────────────────────┘  └──────────────────────┘
                │ each agent writes only its own observations
     pf.agent.lab-8gb · pf.agent.lab-512 · (pf.agent.lab-256, never required)
```

Outside these databases (§9): GitHub, Google Drive, CloudKit (per V0-02) and the LABs' local agent state.

**Why two databases.** PF-03 says operational state belongs to the software that produces it (§3.3) and that observational evidence, including heartbeat and signals, is Antenna's responsibility (§3.9, §3.13). The observation store is therefore declared as Antenna's store under a store-authority contract. It is not a new architectural organ. Coloured Places is a projection over both databases (§3.12).

---

## 2. Registry

### 2.1 The five concepts

The Registry keeps the minimal ontology of Registry Core v0. Tables may carry supporting columns, but no new durable concept is added.

| table | meaning | main columns |
|---|---|---|
| contracts | recognized relationships and definitions, by generation | id, generation, **type**, name, subject, provider, consumer, document digest, effective from/until, recognized at/by, acceptance receipt digest, superseded at/by, retired at |
| entities | what Powerfarm recognizes as existing | id, **type**, name, summary, created at/by, retired at |
| artifacts | things that have exact versions | id, **type**, name, publisher, created at/by, retired at |
| artifact_versions | one exact version | artifact, version, content (digest or manifest digest), source (repository, revision, path), recognized at/by, superseded at/by, retired at |
| grants | explicit authority assigned to one entity | id, subject, **action**, resource, granted by, basis contract, valid from/until, revoked at, reason |

### 2.2 Types come from contracts

**Every type column points to a current contract:**
- contract.type,
- entity.type,
- artifact.type,
- grant.action.

A type exists only while a contract defining it is current. The single exception is the first contract of the Foundation Act, *Contract Type*, which is its own type. Adding a type is one API call that recognizes one contract. It needs no deploy.

Contracts that define types have no subject entity: the definition exists before any entity of that type. Every other contract must name its participants. For example, a mandate names an office and a holder.

### 2.3 Birth order

| phase | what is recognized | table |
|---|---|---|
| **A. First two contracts of the Foundation Act** | 1. *Contract Type* (type: itself) · 2. *Entity Type* (type: Contract Type) | contracts |
| **B. Contract types** | *Artifact Type*, *Action Type*, *Office*, *Mandate*, and the V0 contract families: app-contract, engine-capability, store-authority, search-contract, host-runner, machine-placement, secret-consumer, execution-approval, backup-custody | contracts |
| **C. Enumerations** | entity types · artifact types · action types (below) | contracts |
| **D. Entities** | each entity references the contract of its type; then offices and mandates | entities, contracts |

**V0 entity types** (id forms follow §2.8):

| type | id form | examples |
|---|---|---|
| person | `pf.person.*` | the Director's holder |
| agent | `pf.agent.*` | LLM occupants: the local agents (`pf.agent.lab-8gb`), and LLM sessions acting through a bound credential |
| office | `pf.office.*` | `pf.office.director` |
| sector | `pf.<sector>` | `pf.identity`, `pf.continuity`, `pf.research` |
| machine | `pf.lab-*` | `pf.lab-8gb`, `pf.lab-512` |
| service | `pf.<service>` | `pf.antenna`, `pf.heartime`, `pf.search` |
| host-runner | `pf.host-runner.*` | `pf.host-runner.lab-8gb` |
| process | `pf.process.*` | `pf.process.manhattan` |
| app | `pf.app.*` | `pf.app.coloured-places`, `pf.app.minivault-web` |
| engine | `pf.engine.*` | `pf.engine.google-adk` |
| mcp | `pf.mcp.*` | MCP servers admitted by contract |
| store | `pf.store.*` | `pf.store.supabase.company`, `pf.store.neon.antenna` |
| repository | `pf.repo.*` | Powerfarm-native repositories |
| secret | `pf.secret.*` | secret references (§2.9) |
| search-source | `pf.search-source.*` | per V0-06 |
| projection | `pf.projection.*` | `pf.projection.airtable` |

**V0 artifact types:** document, software, schema, dataset, prompt, capability, execution-bundle, migration-evidence.

**V0 action types:** view, converse, approve, admit-person, recognize-contract, inscribe-entity, grant, store-content, read-content, write-observation.

Each Action Type contract names exactly one **authority** from the institutional vocabulary (OBSERVE · JUDGE · PROPOSE · GENERATE · EXECUTE · ORCHESTRATE · PERSIST · AUTHORIZE), so grants and offices speak one language:

| action types | authority |
|---|---|
| view, read-content | OBSERVE |
| converse | PROPOSE |
| write-observation, store-content, inscribe-entity | PERSIST |
| approve, admit-person, recognize-contract, grant | AUTHORIZE |

### 2.4 Machine-readable contract documents

Each contract generation points to exactly one document: JSON bytes in the Content Store. The Registry verifies the digest before recognizing the generation. The human-readable text and the executable terms live in the same document.

- A **Contract Type** document carries the JSON Schema that documents of that type must satisfy. Creating a new contract type therefore means recognizing one contract that contains its schema.
- An **Entity Type** document declares:
  - the id pattern;
  - **rights** (what every entity of the type may do);
  - **duties** (what it must do);
  - **prerogatives**, such as `hold-mandate`.
- An **Office** document declares which entity types may hold the office and which **powers** it confers.
- A **Mandate** binds one holder to one office for an effective interval. Its id derives from both: `pf.contract.mandate.<office>.<holder>`.

Example: the Entity Type document for *agent*.

```json
{
  "name": "Agent",
  "text": "An agent is a program that observes and acts for Powerfarm at a declared place.",
  "ids": "pf.agent.*",
  "prerogatives": ["hold-mandate"],
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
    rights of the entity's type                        (current Entity Type contract)
  + powers of offices the entity holds                 (current Mandate, only if its type has "hold-mandate")
  + current grants of the entity
```

Mandates are prerogatives of persons and agents in V0. For an office governed by an autonomy matrix (§2.8), what a mandate lets its holder do *without asking* is capped by the rung of each operation class.

Duties are queryable in the same way. The Antenna store compares them with observed facts (§7.3).

### 2.6 Acceptance

Persons accept their Entity Type contract and their mandates. Each acceptance receipt is stored in the Content Store.

- A new generation that only adds rights takes effect without new acceptance.
- A new generation that adds duties requires acceptance again. Until then, the person holds no authority under it.
- The machine decides which case applies by comparing the two generations.

### 2.7 Approval

Consequential effects require explicit authorization under the governing contract. They include destructive machine change, grant issuance, and adoption of a registry target.

Where practical, an approval binds to the exact immutable plan or effect by digest. A materially changed plan requires a new approval.

### 2.8 Offices and the autonomy matrix

V0 has two offices:

| office | held by | meaning |
|---|---|---|
| `pf.office.director` | a person (the owner) | decides, adopts contracts, approves effects |
| `pf.office.engineer` | agents (LLM occupants) | builds, observes, diagnoses, proposes; gains autonomy with time and knowledge |

The Engineer office's charter carries, in machine-readable terms, the **autonomy matrix**: for each **operation class**, the rung at which engineers may act.

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
6. **Evidence is never authored by its subject.** An engineer cannot produce the evidence that promotes it. A rise is a new generation of the Engineer charter, recognized by the Director; a regression may be computed automatically.
7. **The matrix is a resolver, not a rewrite.** It plugs into the runtime's existing approval seam (the agent asks, the resolver answers from the matrix or routes to the Director). Deterministic hand-written rules may exist before any learned rung; evaluations detect when a rung starts deciding wrongly.

**Two edges carry this:**
- **Authority descends:** mandate → grant → run → effect, and never widens.
- **Evidence ascends:** act → receipt → evidence → promotion, and is never authored by its subject.

**The precedent ledger already exists.** The agents' runtime durably records its events, including requests for actions, approval requests and decisions, and results. Every one of these events is copied to the Antenna store with the tool input, the deciding principal and the agent version. The matrix reads that ledger; nothing new has to be invented to feed it.

In V0 every operation class starts at OBSERVE or SUGGEST.

Example (terms of the Engineer charter):

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

Powerfarm ids identify institutional things, not provider objects, filesystem paths or database rows.

- The preferred forms are those in §2.3, plus `pf.contract.*` for contracts.
- Provider identities (Supabase user, Apple, GitHub, machine credential, OAuth subject) are **bindings** to Powerfarm identities. Replacing a provider must not redefine the institutional thing.
- Ids are short, stable and in English. Names and texts may be in Portuguese.

### 2.10 Secrets

The Registry stores **secret references**, never values. A reference is an entity of type *secret*. A contract of family *secret-consumer* declares who may use it. A reference records:
- owner;
- provider or system;
- allowed consumers;
- storage location reference;
- rotation policy;
- revocation path;
- last verification date;
- migration state.

Live secret values must never enter:
- Git;
- Registry rows;
- Search or Airtable projections;
- receipts;
- the Content Store.

Rotation precedes deletion when exposure is possible.

---

## 3. Identity: authentication as a keyring

- **The list of people is the Registry.** The Supabase Auth user table is a keyring: each account is a key, and **every key must be bound to exactly one person entity**.
- **Contact data stays in Identity, never in the Registry.** This includes e-mail.

| table | meaning |
|---|---|
| bindings | login account → person entity (one account per person in V0) |
| admissions | invited e-mail → intended person entity, admitted by, validity, used at |
| acceptances | who accepted which generation of which contract, and when (receipt digest) |

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
  - **Status (researched 2026-09-26):**
    - the Supabase OAuth 2.1 server is beta;
    - open bug `supabase/auth#2820` blocks MCP connectors that use public clients, `offline_access` or the `resource` parameter;
    - tokens are not audience-bound (RFC 8707 is ignored), which MCP 2026-07-28 requires;
    - only Dynamic Client Registration is offered, not Client ID Metadata Documents.
  - The MCP door therefore stays **closed** until this is fixed or an OAuth bridge in front of Identity is adopted. Human sign-in is unaffected.
- Each **agent** has its own machine credential, bound to its agent entity.

---

## 4. Content Store

- **Object:** exact bytes, named `sha256:<hex>`. An object never changes and is never overwritten.
- **Objects table:** digest, size, media type, stored at, stored by (entity).
- **Manifest:** a JSON object listing other objects (`{path, digest, size}`). Compound values (software trees, evidence sets, releases) are manifests. The Registry recognizes the manifest.
- **Storing:** the caller sends bytes, and the API computes the digest and records the object only if it matches.
- **Reading:** a digest is not a capability. Reads go through the API, which asks the Registry whether the caller may read that object, through the artifact or contract that references it, or because it is public.
- **Storing is not recognizing.** An object means nothing institutionally until the Registry recognizes it as an artifact version or a contract document.
- **Where:** a private Supabase Storage bucket owned by `pf.store.supabase.company`.
- **Integrity:**
  - the bucket's access rules allow **insert only**: no update, no delete, so nothing is overwritten;
  - Supabase does not verify content digests, so the API computes SHA-256 server-side before recording an object;
  - a periodic sweep re-hashes stored objects and reports any mismatch.

**Custody:**
- promoted immutable bytes must be addressable and independently verifiable;
- material company bytes need off-machine custody;
- backup policy stays independent of synchronization;
- a redundancy claim requires a distinct failure domain.

---

## 5. Minivault

- Minivault preserves promoted institutional objects (§3.5 of PF-03): typed, immutable revisions behind logical identities, with provenance and relations.
- **Hashes, two roles:**
  - *semantic identity* of a Minivault revision uses **BLAKE3** over canonical JSON;
  - *exact bytes* use **SHA-256** in the shared Content Store.
- Minivault permissions **come from Registry contracts**. There is no separate policy list deciding who may read or write.
- A Minivault publication becomes institutional only when the Registry recognizes it as an artifact version.
- `pf.app.minivault-web` is the human and LLM interface over Minivault: a projection, never a second authority.

---

## 6. Institutional API

The API is the only door. Every call follows the same path: **key → entity → may? → act → record who and when.**

| operation | who may (after the Foundation Act) |
|---|---|
| Foundation Act | nobody: it runs once on an empty Registry and then closes forever |
| recognize a contract or a new generation | holders of *recognize-contract* |
| retire a contract or entity | the same |
| inscribe an entity | holders of *inscribe-entity* for that entity type |
| admit a person | holders of *admit-person* |
| accept a contract | the person concerned |
| grant or revoke | holders of *grant* |
| store and read content | per contract |
| "who am I" and "may I?" | any valid key |

**Foundation Act.** It recognizes the minimum needed for someone to hold authority:
- phases A and B;
- the entity types *person* and *office*;
- the Director's action types;
- the office `pf.office.director`;
- the first person;
- that person's Director mandate;
- that person's admission.

The first person's id and login e-mail are chosen at Foundation and are not recorded in this public document. Everything else (agents, machines, apps, stores, other people, further types) is inscribed afterwards through the API.

---

## 7. Operational: Antenna observation store

`pf.store.neon.antenna` is a Neon Postgres database created through the Vercel integration. It is declared by a store-authority contract with `pf.antenna` as owner.

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

- A read-only projection of types, entities and current contracts with their documents. The principal agent refreshes it through the Registry API; the reserve takes over if the principal is silent.
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

---

## 8. Agents and Host Runners

- **Agents** (`pf.agent.*`) observe, converse and propose. They may hold mandates.
- **Host Runners** (`pf.host-runner.*`) remain the deterministic, allow-listed effect boundary of V0-02, and never treat LLM output as approval.
- An agent and the Host Runner on the same LAB are different entities.
- **LAB 256** is outside the expected ecosystem population (V0-02). An agent may run there, but nothing may depend on it.

---

## 9. Outside the databases

| place | holds | authority? |
|---|---|---|
| GitHub | source, canon, contract drafts | none for contracts: a text counts only after it is stored in the Content Store and recognized. **Transition:** until Minivault documents and `pf.doc.*` recognition exist, the Director's merge adopts canon; afterwards recognition adopts it and GitHub is a projection |
| Google Drive "Powerfarm Backup" | cold archive of the LABs' organized folders | none; items may later be promoted and recognized |
| CloudKit | contract-provisioned app and engine databases (V0-02) | owned by the declaring app or engine |
| LABs | agent queues and credentials | none; rebuildable, except credentials |
| Vercel | Coloured Places (no own state), AI Gateway | none |

**Backups:**
- Identity substrate: provider backups plus a periodic export of the Registry and Content Store to an off-machine destination (to be decided).
- Antenna store: point-in-time restore.

---

## 10. Admission law

A thing belongs in the Registry only when it has an institutional purpose expressible as:
- identity;
- recognized version;
- contract;
- grant;
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
- which grants and mandates permit protected actions;
- which secret reference a consumer requires;
- how it is onboarded, verified, retired and recovered;
- where a promoted object can be resolved and verified;
- which Search sources expose it.

No authority may be inferred from physical presence, provider accounts or connectivity.

---

## 11. Legacy disposition

The previous "current situation" (V0-04) is retired. Legacy sources are disposed of as follows:

| source | disposition |
|---|---|
| Registry schema bootstrapped in `powerfarm.kernal` on 24 Sep 2026 without this plan | `ARCHIVE_THEN_DELETE`: full export (data and original SQL) kept as evidence; schema renamed to legacy with access closed; final deletion performed by the Director |
| observation schema created in `powerfarm.kernal` on 26 Sep 2026 (test data) | same; agents restart in the Antenna store |
| frozen Airtable Registry export (in the Minivault bucket) | becomes the first Content Store object recognized after the Foundation Act |
| legacy Supabase `powerfarm-registry` (source preserved on LAB 8GB) | migration input only for required identity facts; runs, ADK state and workspace drafts do not migrate |
| CloudKit legacy test state | per V0-02 |
| **the book** (Supabase project `vbgzdqdlarulpfsyjrke`, "Google ADK mapping"; 16 schemas, about 186 tables, verified 2026-09-26) | **KEEP.** A reference work Powerfarm acquired. It exists independently, and its existence is not Powerfarm's to decide. It is read, never used as a backend; no DDL; never on a deletion list. It may be recognized as a Research reference |

---

## 12. Build order

| phase | what | done when |
|---|---|---|
| 0 | this plan adopted | the Director merges it |
| 1 | Registry + API + Foundation Act | tests on a throwaway database prove: the first two contracts, the type rule, authority computation, a new generation taking effect immediately, and a Foundation Act that cannot run twice |
| 2 | Identity | the Director signs in; an account without admission is refused; a retired person is blocked |
| 3 | Content Store + manifests | a contract is recognized only when its bytes match the digest; reads without authority are denied |
| 4 | Antenna store | the Registry projection refreshes by itself; the agents write there; both views work |
| 5 | Coloured Places | the Director sees everything the contracts allow |
| 6 | Minivault | on the shared Content Store, governed by contracts |

---

## 13. Open decisions

| # | decision | recommendation |
|---|---|---|
| 1 | login methods per person in V0 | e-mail only |
| 2 | where large bytes (models, archives) live | outside the Content Store in V0; the Content Store holds the manifest pointing to them |
| 3 | initial rung of each Engineer operation class | OBSERVE or SUGGEST for all; protected classes stay gated at every rung |
| 4 | off-machine backup destination for Registry and Content Store exports | to be decided |

**Decided by the Director (2026-09-26):**
- **the book is kept** (§11);
- **offices:** the Director is the owner; LLMs hold the Engineer office and gain autonomy through the matrix (§2.8);
- **Director powers in V0:** everything, gated by approval for protected effects;
- **who admits people:** the Director;
- **Registry in the Antenna store:** an API-refreshed projection, not replication (§7.2);
- **Antenna store cost:** accepted at the researched price.
