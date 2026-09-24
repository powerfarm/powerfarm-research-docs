# V0-01 - Identity, Registry and Minivault

**Status:** WORKING V0  
**Recognition baseline:** `6438c55a20e82e922322d26561487f91761a6e3a`  
**Scope:** V0 materialization of Powerfarm Identity.

## Identity

Identity answers:

> **Who are we?**

For V0, Identity contains three core functions:

- **OAuth / principals / authorization**: who or what may act;
- **Registry**: what Powerfarm recognizes and the structural rules recognized things must satisfy;
- **Minivault**: durable institutional objects Powerfarm chooses to preserve.

These functions share an Identity substrate in V0 but remain semantically distinct.

## Registry: the skeleton

The Registry is normative, not observational.

It records the minimum institutional structure needed to make Powerfarm coherent:

- stable identities;
- recognized artifact/repository versions;
- contracts and contract templates;
- grants and authority;
- ownership and placement relationships;
- declared state stores and their authority;
- provider bindings and durable locators;
- references to promoted Minivault objects.

It does **not** attempt to contain:

- ordinary application rows;
- workflow chatter;
- every experiment event;
- logs or telemetry;
- every repository edit;
- every operational database mutation.

The rule is:

> **The Registry does not need to know what everyone is doing. It requires recognized things to do it through the declared contracts and forms.**

Operational truth remains with the software that owns it.

## Minivault: the promotion boundary

Most daily Powerfarm activity is intentionally local, mutable and disposable. Some of it becomes institutionally valuable.

```text
daily work
   ↓
valuable durable result
   ↓
promote
   ↓
Minivault
   ↓
optional Registry recognition / relationship
```

Minivault preserves the semantics and provenance of promoted objects independently of a particular storage engine.

V0 preserves these invariants from the current kernel work:

- canonical semantic identity, currently using BLAKE3;
- exact byte/content identity, currently using SHA-256 where content addressing is required;
- immutable revisions;
- logical aliases/heads;
- provenance and relations;
- validation, review and publication;
- preconditioned/compare-and-swap publication where required;
- storage backends do not become ontology merely by holding records.

Exact immutable bytes may be stored separately from their semantic records, but they remain independently verifiable.

## Powerfarm repositories

A **Powerfarm Repository** is an institutional software object, not necessarily a GitHub repository.

Working V0 direction:

- Powerfarm-native repository identity, versions, relations and provenance belong to Identity/Minivault;
- exact repository objects or bundles may use Supabase Storage or another adopted immutable byte substrate;
- GitHub may be used as a collaboration, source projection, publication or interoperability surface;
- a GitHub repository does not define the Powerfarm-native repository format merely because the two are synchronized.

The exact native repository schema is implementation work. Provider choice must not redefine repository identity.

## Supabase Identity substrate

Working V0 binds `pf.store.supabase.company` to:

- project ref: `ekjlmclhqnsstfjzuabz`
- provider-side name: `powerfarm.kernal`
- region: `eu-west-1`

The provider name is not the institutional identity.

This project is the V0 destination for Identity materialization: OAuth/principals, Registry, Minivault metadata/objects and supporting Identity state. The exact database/kernel schema is still being built.

At first census it contained no Powerfarm user migrations, Storage buckets, Edge Functions, Auth users or development branches and is therefore treated as a clean destination substrate.

### Legacy Supabase migration

A separate historical Supabase project named `powerfarm-registry` is a migration source, not a V0 authority.

Its exact contents require a read-only census before migration. The rule is:

```text
legacy powerfarm-registry
  → identify required institutional truth
  → migrate to V0 Identity
  → verify identities / relationships / receipts
  → retire and disregard the legacy project
```

Powerfarm does not modernize the legacy project in place.

## Minivault Web

V0 requires a human/LLM-facing Minivault application, `pf.app.minivault-web`.

Its purpose is to let intelligent systems and the Director store, discover and retrieve promoted software/repository objects and other durable Minivault content without exposing raw database internals.

The app is a projection/interface over Identity/Minivault, not a second authority. It should expose stable object identity, provenance, versions/heads, relationships and exact-byte retrieval where permitted.

## Search and Airtable

Powerfarm Search is a federated read model over recognized sources.

Search:

- discovers sources through Registry/contracts;
- preserves source identity, locator, freshness and provenance;
- does not own canonical state;
- may be rebuilt.

Airtable is the human frontend/projection of Search.

The current Registry-shaped Airtable base is a migration source. Required Registry truth moves to Supabase, migration is verified, the old Registry tables/records are deleted, and Airtable is rebuilt as Search.

Manual Airtable edits must not directly mutate Registry authority.

## Storage and custody

Storage and backup are implementation concerns under declared ownership.

V0 requires:

- promoted immutable bytes to be addressable and independently verifiable;
- material company bytes to have durable off-machine custody;
- backup policy to remain independent of synchronization;
- redundancy claims to require a distinct failure domain.

No specific second provider is canon.

CloudKit is **not** the Identity/Registry substrate in final V0. Its V0 role is defined by Continuity in V0-02.

## Exit criteria

Identity V0 is sufficiently materialized when:

1. the destination Supabase project implements the recognized Identity contracts;
2. required truth from legacy Supabase and Airtable Registry sources has been migrated and verified;
3. the legacy Supabase Registry and old Airtable Registry materializations are retired;
4. Minivault promotion and retrieval preserve identity, provenance and exact-byte verification;
5. Search can explain recognized sources without becoming authority;
6. no provider name or storage engine is required to define institutional identity.
