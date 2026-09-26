# Negative Delta Execution — Tranche 2 / Identity Migration Bridge

**Date:** 24 September 2026  
**Authority:** frozen C from PR #8 and execution continuation after merged PR #9.  
**Purpose:** build only the minimum Identity/Registry/Minivault substrate required to retire legacy authority safely.

## Registry Core installed on powerfarm.kernal

Supabase project:

- project ref: `ekjlmclhqnsstfjzuabz`
- provider name: `powerfarm.kernal`

Applied migrations:

1. `registry_core_v0_private`
2. `registry_core_v0_bootstrap_entities`
3. `registry_v0_manifest_entities_and_legacy_airtable_evidence`
4. `minivault_private_bucket_and_security_hardening`

Registry Core implements only the five concepts defined by `powerfarm-specs/specs/REGISTRY_CORE_v0.md`:

- entities
- artifacts
- artifact_versions
- contracts
- grants

It does not contain Continuity runtime state, app rows, Search state, workflow events, old gadget/workspace state or legacy operational tables.

## Security boundary

- schema: `powerfarm_registry`
- RLS enabled on all five tables
- no `anon` or `authenticated` policies yet
- schema/table/function access revoked from public client roles
- current views use `security_invoker`
- material artifact/contract identity is trigger-protected against silent mutation
- helper functions have fixed empty `search_path`
- pre-existing public execute access to `public.rls_auto_enable()` was revoked from public/anon/authenticated

The remaining Supabase advisor notices are informational: RLS is intentionally enabled with no client policies while Registry mutation remains private.

## Current Registry counts

Verified state after migration:

- entities: **14**
- artifacts: **1**
- artifact versions: **1**
- contracts: **0**
- grants: **0**

The zero contract/grant count is deliberate.

## Frozen V0 identities bootstrapped

Recognized stable identities include:

- `pf.person.director`
- `pf.research`
- `pf.continuity`
- `pf.identity`
- `pf.lab-8gb`
- `pf.lab-512`
- `pf.app.coloured-places`
- `pf.process.manhattan`
- `pf.app.minivault-web`
- `pf.antenna`
- `pf.heartime`
- `pf.search`
- `pf.host-runner.lab-8gb`
- `pf.host-runner.lab-512`

Entity existence does not imply runtime admission; it establishes institutional identity only.

## Airtable migration classification

Legacy base:

- id: `appxhcqgkAaI2qkaa`
- name: `Powerfarm - LLM Engineering Benchmark Powerplant`

Current direct Registry-shaped counts:

- REGISTRY_ITEMS: 58
- ARTIFACTS: 0
- CONTRACTS: 1
- GRANTS: 5
- CONTRACT_TERMS: 6
- REGISTRY_RELATIONS: 34
- PERMISSIONS: 7
- CAS_OBJECTS: 64

### What migrates

The frozen V0 target, not legacy Airtable status labels, decides survival.

The old Airtable base is preserved as migration evidence instead of copying its full ontology into Registry Core.

### What does not migrate

The only Airtable contract governs the retired Capacity Registry.

All five grants authorize either:

- the retired MCP Portal; or
- the retired Capacity Registry / old CAS-read behavior.

Therefore **zero legacy Airtable contracts and zero legacy Airtable grants are migrated as live V0 authority**.

Old Capacity Registry objects, MCP Portal identities, LAB 256 territories, old onboarding/check objects and legacy Unknowns are not resurrected merely because Airtable marked them Active.

## Frozen Airtable evidence artifact

Registered:

- artifact: `pf.artifact.legacy-airtable-registry-export`
- version: `2026-09-23`
- digest: `sha256:0ea09c53bc59512118c69f60f7572d19ae2e48c0cbf23bf183c033bd2863e9ec`
- frozen table count: 38
- frozen record count: 347

This records the exact historical evidence boundary without making Airtable live authority.

The exact frozen export bytes were not found under the obvious LAB 8GB paths during this tranche, so Airtable is **not yet deleted**. A fresh durable export/custody step remains required before destructive Airtable retirement.

## Minivault substrate

Created private Supabase Storage bucket:

`powerfarm-minivault`

Verified:

- bucket exists
- `public = false`

No broad client upload/read policy has been opened yet.

## Coloured Places

Post-cleanup verification on LAB 8GB:

- launch label `com.minilab.app.places` remains loaded
- HTTP service on `127.0.0.1:4176` responds (HTTP 307 redirect)

Coloured Places therefore survived the negative-delta cleanup and is actively serving.

## Remaining cleanup blockers

Before deleting the old Airtable Registry materialization:

1. produce/store a fresh deterministic full Airtable export in durable Minivault custody;
2. verify the stored export digest and retrievability;
3. preserve/promote any research output specifically chosen as institutional gold;
4. only then delete/rebuild the Airtable base as Powerfarm Search.

Provider cleanup still pending separately:

- delete empty Supabase project `Google ADK mapping` once the correct provider account management surface is available;
- reset historical CloudKit test data/schema while preserving/recreating Apple provisioning capability.

## Result

The company now has a real V0 Registry skeleton and private Minivault storage substrate on `powerfarm.kernal`.

Legacy Airtable authority has been classified, but not yet destructively removed.

This tranche intentionally avoids rebuilding old operational architecture inside Identity.
