# V0-06 — Powerfarm Search

**Status:** WORKING V0, deferred. Built after waves 1–3 of [V0-00](V0-00_DELTA_AND_PLAN.md).
**Canon:** PF-03 §3.12

Target for Powerfarm Search: the read model over recognized Powerfarm sources, at `search.powerfarm.app` (V0-07).

---

## 1. Purpose

Powerfarm Search answers:

> **What can we discover about Powerfarm without moving authority into the search surface?**

Search is a read model. It MUST NOT become a store of record, a migration target, or a hidden second Registry.

```text
sources of truth
      ↓
source connectors
      ↓
Search projection
      ↓
human interface
```

If the projection or its interface disappears, no institutional fact changes.

---

## 2. Sources

### 2.1 V0 sources

| source | what Search may project | authority stays with |
|---|---|---|
| **Identity substrate** | recognized, non-secret Registry information; Minivault metadata and names suitable for discovery | the Registry and Minivault |
| **App and engine databases** | contract-declared, non-secret metadata from admitted app and engine databases (including CloudKit namespaces) | the owning app or engine |

Search never infers ownership from physical presence. Ownership comes from contracts.

### 2.2 Adding a source

GitHub, Cloudflare, Braintrust and other systems MAY become sources. Being useful or connectable is not enough: a new source requires an adopted source contract that defines:

- source identity;
- authoritative scope;
- projected fields;
- stable source key;
- freshness semantics;
- sensitivity exclusions;
- rebuild behavior.

---

## 3. Projection identity

- A projected thing that has a Powerfarm name keeps it: `powerfarm.app/<type>/<name>` (V0-07).
- Anything else gets a deterministic key: `<source>:<kind>:<source-stable-id>`.
- Record ids of the interface never become Powerfarm identity.

---

## 4. The projection

One unified discovery surface. Required fields:

- name or projection key;
- source;
- kind;
- title;
- short summary, when available;
- recognized version and digest, when relevant;
- freshness (last seen);
- source link, when safe;
- an explicit `projection-only` marker.

Domain-specific detail MAY live in linked projection tables when real use requires it. Tables are not created merely because the source has tables.

---

## 5. Connectors

Each source connector MUST:

1. enumerate or pull source changes;
2. map only the declared projection fields;
3. produce the deterministic key (§3);
4. write idempotently;
5. record its own freshness and health;
6. support a full rebuild;
7. exclude credentials and restricted values.

Provider rate limits and batch sizes belong in connector configuration, not in this document.

---

## 6. Rules

### 6.1 Rebuildable

Search MUST be fully reconstructable from its sources:
- no record exists only in the projection;
- edits in the interface never change a source;
- a full rebuild recreates the projection;
- losing the whole projection is a recoverable loss, not a loss of institutional data.

### 6.2 Read-only toward sources

Search never writes to a source. A future interface action MAY create a proposal through the institutional API; the proposal passes the authority and contract boundary like any other act.

### 6.3 Security

Search MUST NOT project:
- secret values;
- tokens;
- private keys or certificates;
- credentials;
- fields excluded by the governing contract.

Security happens at source selection and authorization, never by hiding fields in the interface.

### 6.4 Freshness

Each connector exposes enough evidence to distinguish:
- the source has no change;
- the projection is current;
- the connector is stale or broken;
- the source could not be reached.

A stale connector never makes stale data look current.

### 6.5 Mobile

The Director uses Search on an iPhone. Any mobile-critical behavior is tested on a physical iPhone before it becomes an acceptance condition.

---

## 7. Acceptance

Search conforms when:

1. **Rebuild:** a deleted projection is reproduced with the same set of keys and digests.
2. **Idempotency:** a source object delivered twice produces one projection record.
3. **Authority:** changing or deleting projection records changes no source.
4. **Secrets:** known secret values never appear in the projection.
5. **Freshness:** a stopped connector becomes visibly stale.
6. **Mobile:** the required views work on the Director's iPhone.
7. **Scope:** every projected record names its source and its projection rule.

---

## 8. Not in V0

- a universal schema observatory;
- automatic drift detection;
- GitHub and Cloudflare connectors;
- AI-generated summaries;
- two-way sync.
