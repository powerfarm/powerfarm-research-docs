# V0-06 — Powerfarm Search

**Status:** WORKING V0  
**Scope:** the disposable human/search projection over recognized Powerfarm sources.

## Purpose

Powerfarm Search answers:

> **What can we discover about Powerfarm without moving authority into the search surface?**

Search is a read model.

It MUST NOT become a store of record, migration target, or hidden second Registry.

```text
sources of truth
      ↓
Search connectors
      ↓
Powerfarm Search projection
      ↓
Airtable human interface
```

If Airtable disappears, no institutional fact changes.

## V0 authoritative sources

V0 Search reads from two source families.

### Supabase Identity

Search may project recognized, non-secret information from:

- Registry;
- Minivault metadata and locators appropriate for discovery.

Supabase remains authority for that information.

### Apple / CloudKit

Search may project contract-declared, non-secret metadata from admitted App/Engine databases or namespaces.

The owning app/engine remains authority for its operational state.

Search does not infer app ownership from physical CloudKit presence. Ownership comes from Identity/contracts.

## Additional sources

GitHub, Cloudflare, Braintrust and other systems MAY become Search sources later.

They are not V0 sources merely because they are useful or technically connectable.

A new source requires an adopted connector/source contract defining:

- source identity;
- authoritative scope;
- projected fields;
- stable source key;
- freshness semantics;
- sensitivity exclusions;
- backfill/rebuild behavior.

## Projection identity

Every projected object has a source-stable key.

Airtable record IDs MUST NOT become Powerfarm identity.

Working form:

```text
<source>:<kind>:<source-stable-id>
```

The exact encoding may evolve, but it must remain deterministic and independent of Airtable.

## Rebuildability

Powerfarm Search MUST be fully reconstructable from its sources.

Therefore:

- no record may exist only in Airtable;
- Airtable edits MUST NOT directly mutate source authority;
- connector backfill must be able to recreate the projection;
- losing the entire Airtable base is a recoverable projection loss, not institutional data loss.

## Write boundary

V0 Search is read-only toward sources.

A future UI action MAY create a proposed command/request through a separately authorized Powerfarm API or workflow.

That proposal is not a direct source mutation and MUST pass the authority/contract boundary before execution.

## Connector responsibilities

Each source connector MUST:

1. enumerate or pull source deltas;
2. map only declared projection fields;
3. generate a deterministic projection key;
4. upsert idempotently;
5. record connector freshness/health;
6. support full backfill/rebuild;
7. exclude credentials and source-restricted sensitive values.

Provider-specific rate limits and batch sizes belong in connector configuration/runbooks, not canon.

## Search projection model

The minimal V0 projection needs one unified discoverability surface.

Required projected fields:

- stable projection key;
- source;
- kind;
- title/name;
- short description/summary when available;
- recognized version/digest when relevant;
- freshness/last-seen evidence;
- source locator/deep link when safe;
- explicit `projection-only` authority marker.

Additional domain-specific detail MAY live in linked projection tables if real product use requires it.

Do not create tables simply because the source has tables.

## Airtable role

Airtable is the current human projection/frontend of Powerfarm Search.

The current base has already been reduced to a single `Powerfarm Search` table after verified Minivault custody of the legacy 38-table/347-record export.

Airtable is selected because it currently provides useful human/mobile interfaces without requiring Powerfarm to build a custom frontend first.

Airtable-specific layout, automation, AI and plan limits are dated provider behavior and belong in research/runbooks.

## Mobile rule

The Director must be able to use the Search interface on iPhone.

Any mobile-critical behavior MUST be tested on a physical iPhone before it becomes an acceptance dependency.

Required slices should be shipped as stable views/tabs/quick filters rather than assuming desktop filtering/grouping behavior exists on iOS.

## Security

Search MUST NOT project:

- secret values;
- tokens;
- private keys/certificates;
- credentials;
- source fields excluded by the governing contract;
- sensitive data merely hidden by Airtable interface cosmetics.

Security happens at connector selection and source authorization, not by hiding fields in Airtable.

## Freshness

Each connector must expose enough health/freshness evidence to distinguish:

- source has no change;
- projection is current;
- connector is stale/broken;
- source could not be reached.

A stale connector must not make stale projection data appear current.

## Acceptance checks

V0 Search is conforming when:

1. **Rebuild:** delete a disposable test projection and reproduce the same projected key/digest set from sources.
2. **Idempotency:** deliver one source object twice and produce one projection record.
3. **Authority:** changing/deleting Airtable projection records changes no source state.
4. **Secrets:** known secret-reference values never appear in the projection.
5. **Freshness:** a stopped connector becomes visibly stale rather than silently current.
6. **Mobile:** required Search views work on the Director's physical iPhone.
7. **Source scope:** every projected row can name its source and governing projection rule.

## Current implementation state

As of 24 September 2026:

- Airtable contains one `Powerfarm Search` table;
- the initial projection contains Supabase Registry and Minivault objects;
- CloudKit is a declared source class but final app/engine databases have not yet been provisioned;
- Airtable is not authority;
- the pre-retirement Airtable dataset is preserved in Minivault with verified round-trip SHA-256 custody.

## Non-goals for V0

Not required yet:

- a universal schema observatory;
- automatic drift/lint engine;
- GitHub/Cloudflare connectors;
- AI-generated summaries;
- Omni workflows;
- a custom Powerfarm Search web application;
- two-way sync.

Those remain valid future research/product directions.
