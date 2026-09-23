# V0-01 - Minivault, Storage and Registry

**Status:** PROPOSED until merged to `main`  
**Scope:** V0 materialization of PF-03/PF-04 architecture.  
**Owner:** Powerfarm / Director.

## Decision

Powerfarm V0 separates semantic authority, company-wide recognition, project-local semantic worlds, immutable bytes, execution state and human projections.

```text
                        POWERFARM V0

        company / institutional plane
                  Supabase
                     |
          Registry + authority + ops
                     |
                     +------ Powerfarm Search ------> Airtable
                     |              ^
                     |              |
                     |          CloudKit sources
                     |
        project / LAB-adjacent plane
              CloudKit / Minivault
```

The two data planes are not duplicate truths.

- **Supabase** is the company control plane: institutional Registry, grants/authority, operational automation state, adopted/published cross-project state, Search coordination and durable company-wide projections.
- **CloudKit** is the Apple/LAB-adjacent project-vault plane: project-local Minivault worlds, immutable revisions, heads, relations and CKAssets where appropriate.
- **Minivault** owns semantic identity and invariants. A storage engine does not redefine Minivault semantics.
- **Powerfarm Search** is the federated read model across recognized stores. It never becomes authority.
- **Airtable** is a human projection of Powerfarm Search and may be rebuilt.

## Minivault invariants

The current Minivault kernel establishes a storage-independent semantic layer. V0 preserves:

- canonical semantic identity with BLAKE3;
- transport/content identity with SHA-256 where exact bytes are addressed;
- immutable revisions;
- logical aliases/heads;
- provenance, relations, validation, review and publication;
- compare-and-swap or equivalent preconditioned publication;
- no storage backend becoming ontology merely by holding records.

The V0 implementation SHOULD expose explicit read/commit ports rather than require whole-world snapshot transactions when a remote backend cannot provide them naturally.

## Supabase company plane

V0 intends one Powerfarm Supabase project as the central company control plane.

Expected logical homes:

- `registry`: institutionally recognized entities, artifacts, artifact versions, contracts, grants, capacities, placements, territories, census observations and related recognition state;
- `vault`: adopted/published company-wide Minivault objects when they genuinely belong at company scope;
- `ops`: jobs, receipts, requests, findings, health and delta execution state;
- `projection`: rebuildable Search/Airtable projector state;
- `private`: material that must not be exposed through normal data APIs.

The exact schema is implementation, but the ownership split is part of this V0 specification.

## CloudKit project-vault plane

The existing Apple implementation identifies container:

`iCloud.app.powerfarm`

The historical implementation uses the Public Cloud Database and includes:

`PFEntity`, `PFPrincipal`, `PFGrant`, `PFPlace`, `PFContract`, `PFArtifact`, `PFArtifactVersion`, `PFApplication`, `PFRecognition`, `PFBinding`, `PFSoftware`, `PFContent`, and `PFHead`.

V0 direction:

- project semantic worlds SHOULD use CloudKit where the Apple/LAB relationship makes it advantageous;
- project-local records SHOULD be isolated by explicit locator: container + environment + database scope + zone;
- private/custom zones are preferred for project worlds that must not be public;
- `PFContent`/CKAsset or a successor adapter MAY implement exact immutable byte storage, but Minivault ContentRef semantics remain backend-independent;
- CloudKit record identity MUST NOT replace PFID, Minivault logical identity or content digests;
- local filesystem databases are not the default project authority merely because the project runs on a Mac.

The previously proposed zone name `PowerfarmInstitution` is historical design input, not yet treated as a proven live resource. V0 may adopt a different zone/sharding layout after live CloudKit inventory.

## Powerfarm Search

Powerfarm Search is the federated read model defined by PF-03:

```text
query
  -> Registry / recognized relationships
  -> recognized Search surfaces
  -> authorization boundary
  -> federated reads
  -> normalized results + provenance
```

V0 Search MUST preserve at least:

- source store/application;
- canonical subject/artifact identity;
- source locator;
- query/freshness time;
- authority/contract reference where relevant;
- material/content reference where relevant;
- provenance sufficient to explain why the result exists.

Search indexes and projector state are disposable. Their loss MUST NOT erase canonical state.

### Search sources in V0

- Supabase SearchSource: company Registry, adopted objects, ops/health and searchable company-wide state.
- CloudKit SearchSource: recognized project-vault surfaces reached through an Apple-authenticated client/agent where required.
- Future stores may implement SearchSource without changing the Search model.

## Airtable projection

Airtable is a projection of **Powerfarm Search**, not an independent replica of every backend.

V0 Airtable should expose a compact human surface such as:

- SEARCH
- SOURCES
- HEALTH
- REQUESTS
- ACTIVITY

Airtable rows MUST carry stable canonical/source locators and freshness/provenance sufficient to trace the row back to its owner.

Manual Airtable edits MUST NOT directly mutate Registry authority. Write intent enters through a request/approval path.

## Immutable bytes and custody

Storage and backup are distinct concerns.

V0 requires:

- exact immutable bytes to be addressable and independently verifiable;
- at least one off-machine durable copy for material company bytes during bootstrap;
- backup policy to remain independent of synchronization semantics;
- a second failure domain for material company truth before any copy is called redundant.

The exact second provider is not canon. AWS S3 is not mandatory. iCloud/CloudKit, Cloudflare R2, S3-compatible storage or another independently verifiable store may satisfy the role when explicitly adopted.

## V0 exit criteria

This specification is sufficiently materialized when:

1. Supabase company plane is live and identified.
2. CloudKit project-vault locator policy is adopted and at least one real project round-trips through it.
3. Minivault semantic conformance tests pass against each adopted store adapter.
4. Powerfarm Search federates at least Supabase + CloudKit with provenance.
5. Airtable is generated from Search rather than treated as authority.
6. Backup/custody rules are verified by restore/hash evidence.
