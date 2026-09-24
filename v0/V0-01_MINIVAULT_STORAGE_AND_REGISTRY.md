# V0-01 - Minivault, Storage and Registry

**Status:** WORKING V0, recognized at `6438c55a20e82e922322d26561487f91761a6e3a`  
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
- **CloudKit** is the Apple/LAB-adjacent application database substrate: final V0 contains only databases owned by admitted Ecosystem Apps. Historical Registry/test material is not part of the target.
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

Working V0 binds `pf.store.supabase.company` to the existing Supabase project:

- project ref: `ekjlmclhqnsstfjzuabz`
- provider-side name: `powerfarm.kernal`
- region: `eu-west-1`
- observed state on 23 September 2026: `ACTIVE_HEALTHY`
- PostgreSQL: 17.6.1.166 / engine 17

The provider-side spelling does not define Powerfarm identity. The stable institutional identity is `pf.store.supabase.company`.

At first census the project had zero user migrations, zero Storage buckets, zero Edge Functions, zero Auth users and zero development branches. It is therefore treated as a clean, unmaterialized V0 substrate rather than a legacy database to untangle.

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

- admitted Ecosystem Apps MAY use CloudKit for app-owned databases where the Apple/LAB relationship makes it advantageous;
- each Ecosystem App database SHOULD be isolated by explicit locator: container + environment + database scope + zone;
- private/custom zones are preferred for project worlds that must not be public;
- `PFContent`/CKAsset or a successor adapter MAY implement exact immutable byte storage, but Minivault ContentRef semantics remain backend-independent;
- CloudKit record identity MUST NOT replace PFID, Minivault logical identity or content digests;
- local filesystem databases are not the default project authority merely because the project runs on a Mac.

The previously proposed zone name `PowerfarmInstitution` is historical design input, not yet treated as a proven live resource. V0 may adopt a different zone/sharding layout after live CloudKit inventory.

### CloudKit deletion law

The historical Public Database Registry/test material is **negative delta with terminal disposition `DELETE`**.

Before deletion, Powerfarm preserves only the evidence needed to prove what existed and, where applicable, migrates any still-authoritative content into its V0 owner. The frozen census/receipts are the historical record; CloudKit itself is not the archive.

At V0 convergence:

- no historical `PFEntity`, `PFPrincipal`, `PFGrant`, `PFPlace`, `PFContract`, `PFArtifact`, `PFArtifactVersion`, `PFApplication`, `PFRecognition`, `PFBinding`, `PFSoftware`, legacy `PFContent`, or legacy `PFHead` test material remains merely because an old test created it;
- any CloudKit data that remains belongs to an admitted Ecosystem App database and is declared by that app's contract;
- institutional Registry authority lives in Supabase, not CloudKit.

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

### Airtable deletion/rebuild law

Today's Airtable Registry is a **migration source**, not a legacy system to retain.

The transition is:

```text
current Airtable Registry
  -> classify authoritative rows
  -> migrate/recognize in Supabase Registry
  -> verify counts, identities, relationships and receipts
  -> DELETE old Airtable Registry tables/records
  -> rebuild Airtable as the Powerfarm Search frontend
```

The frozen Airtable export and migration receipts preserve history. The old Registry materialization itself is deleted after verification. Final Airtable contains only Search/projection surfaces and related non-authoritative request/health views.

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
7. Historical CloudKit Registry/test records are deleted; remaining CloudKit data belongs only to admitted Ecosystem Apps.
8. The old Airtable Registry materialization is deleted and Airtable has been rebuilt as the Powerfarm Search frontend.
