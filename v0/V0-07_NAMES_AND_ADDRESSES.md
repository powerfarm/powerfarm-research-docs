# V0-07 — Names and Addresses

**Status:** WORKING V0, proposed for Director adoption
**Date:** 26 September 2026
**Canon:** PF-03 §3 (vocabulary); V0-01 §2.3, §2.4, §2.9
**Replaces:** the `pf.*` id forms in V0-01, V0-02 and `registry-v0.yaml`, and V0-01 §2.9 (Names)

---

## 0. Principle

**One name per thing. The name is the identity, the address and the link, and it says Powerfarm in full.**

Powerfarm has three kinds of names:

| Kind | Form | Example |
|---|---|---|
| **Things** that Powerfarm recognizes | `powerfarm.app/<type>/<name>` | `powerfarm.app/agent/lab-8gb` |
| **Services** you connect to | `<service>.powerfarm.app` | `id.powerfarm.app` |
| **Bytes** | `sha256:<hex>` | `sha256:9f2c…` (64 hex digits) |

A name says *what*, a digest says *exactly which bytes*, and a version binds the two.

---

## 1. Things: `powerfarm.app/<type>/<name>`

### 1.1 Grammar

```text
thing    = "powerfarm.app/" type "/" name [ "@" version ]
type     = [a-z][a-z0-9-]{0,39}
name     = [a-z0-9] ( [a-z0-9.-]{0,98} [a-z0-9] )?     no "..", no "--"
version  = [a-z0-9][a-z0-9.+-]{0,39}
```

- Always exactly two path segments after the host. Hierarchy inside a name uses dots: `mandate.director.<holder>`, `intake.review`.
- Lowercase ASCII only, so there is never a case question.
- **Stored without a scheme.** Putting `https://` in front **resolves** it: the answer is the thing's card, or "not allowed" when the Registry says the caller may not view it.
- No trailing slash, no query string, no fragment inside an id.

### 1.2 Contracts live under `/contract/`, everything else under its type

Contracts define the types, so they form one family:

```text
powerfarm.app/contract/contract-type        the first contract; its type is itself
powerfarm.app/contract/entity-type          the second
powerfarm.app/contract/person               defines the entity type "person"
powerfarm.app/contract/program              defines the artifact type "program"
powerfarm.app/contract/mandate.director.<holder>
powerfarm.app/contract/entity-type@2        a generation
```

Every entity and artifact lives under the **type its contract defines**. The type segment is the name of that contract:

```text
powerfarm.app/person/<holder>        its type is defined at powerfarm.app/contract/person
powerfarm.app/agent/lab-8gb          …at powerfarm.app/contract/agent
powerfarm.app/machine/lab-8gb        …at powerfarm.app/contract/machine
powerfarm.app/office/director        …at powerfarm.app/contract/office
powerfarm.app/store/company          …at powerfarm.app/contract/store
powerfarm.app/program/intake.review  a Minivault item; "program" is an artifact type
powerfarm.app/document/pf-03@1.3     a canon document at an exact version
```

**Asking "what is a person?"** means opening `powerfarm.app/contract/person`.

Type names are unique across all families (entity, artifact and action types), because each is one contract.

### 1.3 Names say *what*, never *where*

A name never carries a provider, a machine, a storage location or a technology. Replacing a provider must not rename the thing.

Example: the Identity substrate is `powerfarm.app/store/company`, whichever provider hosts it.

### 1.4 Names are forever

- A name is never reused, even after the thing is retired.
- A name is never changed. If a thing truly needs a different name, it becomes a new entity, and the old one is retired with a pointer to the new one.

### 1.5 Other named records

- Grants: `powerfarm.app/grant/<uuid>`
- Acts in the act log: `powerfarm.app/act/<sequence>`

Both are resolvable, for receipts and links.

### 1.6 People and provider identities

- The first person's name is chosen at the Foundation Act and is not recorded in public documents (V0-01 §6).
- A person's e-mail may match their name by convention (`<name>@powerfarm.app`). The e-mail stays a login key in Identity, never the identity (V0-01 §3).
- Provider identities (Supabase user, Apple, GitHub, machine credential, OAuth subject) are **bindings** to names, never names themselves.

---

## 2. Bytes: `sha256:<hex>`

- Exact bytes are named by their SHA-256 digest, in lowercase hex, 64 digits.
- The digest identifies content; it is not a capability (V0-01 §4).
- Resolvable through the API at `powerfarm.app/content/sha256:<hex>`, subject to the Registry.

---

## 3. Services: `<service>.powerfarm.app`

### 3.1 Rules

1. **A subdomain exists only for something you connect to**: a running service with an owner entity and a contract. People, contracts, documents and machines never get subdomains. Subdomains are public (every hostname with a certificate is published in certificate logs); paths are not listed.
2. **One word, lowercase, naming the role.** Never a provider, a machine or a technology.
3. **Each service is itself a Registry entity** (`powerfarm.app/service/<x>` or `powerfarm.app/app/<x>`), and its contract names its hostname.
4. **Previews** use `<service>-preview.powerfarm.app`.
5. **`powerfarm.app` is first-party only.** Generated or untrusted apps never live under it, so they can never read Powerfarm's login cookies. They get a separate domain when they appear.
6. **One passkey for all of Powerfarm:** the WebAuthn relying-party ID is `powerfarm.app`, so a passkey made at `id.powerfarm.app` works on every Powerfarm service.

### 3.2 The services

| Hostname | What it is | Registry entity |
|---|---|---|
| `powerfarm.app` | **The front door and name resolver.** Every `powerfarm.app/<type>/<name>` opens here | `powerfarm.app/service/registry` |
| `id.powerfarm.app` | **Identity:** login, OAuth 2.1 issuer, consent | `powerfarm.app/service/identity` |
| `api.powerfarm.app` | **The institutional API:** Registry, Content Store and Minivault functions (the only door) | `powerfarm.app/service/api` |
| `vault.powerfarm.app` | **Minivault web:** the human and LLM view (a projection) | `powerfarm.app/app/minivault-web` |
| `places.powerfarm.app` | **Coloured Places** | `powerfarm.app/app/coloured-places` |
| `mcp.powerfarm.app` | **The MCP door** for ChatGPT and Claude. Later: closed until the Supabase OAuth fix (V0-01 §3) | `powerfarm.app/service/mcp` |
| `search.powerfarm.app` | **Search** (V0-06). Later | `powerfarm.app/service/search` |

A hostname not in this table has no place in V0.

---

## 4. Type names used in V0

**Entity types:**
- `person`, `agent`, `office`, `sector`, `machine`, `service`, `host-runner`, `process`, `app`, `engine`, `mcp`, `store`, `repository`, `secret`, `search-source`, `projection`

**Artifact types:**
- from V0-01: `document`, `software`, `schema`, `dataset`, `prompt`, `capability`, `execution-bundle`, `migration-evidence`
- from Minivault: `program`, `component`, `knowledge`, `idea`, `decision`, `trajectory`, `unknown`

**Action types:**
- `view`, `converse`, `approve`, `admit-person`, `recognize-contract`, `inscribe-entity`, `grant`, `store-content`, `read-content`, `write-observation`

**Minivault's older kinds meet the Registry here:**
- `contract` becomes the artifact type `schema`;
- `repository` is the entity type `repository`;
- `identity` and `authority` are Registry entities and grants, not artifact types.
