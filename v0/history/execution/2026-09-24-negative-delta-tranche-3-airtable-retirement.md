# Negative Delta Execution — Tranche 3 / Airtable Retirement

**Date:** 24 September 2026  
**Authority:** Identity migration bridge recognized by merged PR #10, merge commit `103809ed10327d4ee3a35c7c216df2b55c513fa7`.

## Deterministic pre-retirement export

A fresh full export of the legacy Airtable base was produced before deletion.

Source base:

- base id: `appxhcqgkAaI2qkaa`
- historical name: `Powerfarm - LLM Engineering Benchmark Powerplant`
- tables: **38**
- records: **347**

Export format:

- NDJSON
- one manifest line
- 38 table-schema lines
- 347 record lines
- object keys sorted lexicographically
- tables ordered by name/id
- records ordered by Airtable record id

Local custody receipt:

`~/POWERFARM/.receipts/airtable-retirement-20260924/airtable-full-export.ndjson`

Size:

`537688` bytes

SHA-256:

`35214d1dae9c79fc05256da00a797f3b0d4c0eca5e00921108502c070b8a36d2`

## Minivault custody

The exact export was uploaded to the private Supabase Storage bucket:

- bucket: `powerfarm-minivault`
- object: `migration/airtable/2026-09-24/airtable-full-export.ndjson`

A temporary Storage policy allowed only this exact object path for the migration operation.

The object was downloaded again and hashed on LAB 8GB.

Round-trip SHA-256:

`35214d1dae9c79fc05256da00a797f3b0d4c0eca5e00921108502c070b8a36d2`

The source and round-trip hashes matched exactly.

The temporary Storage INSERT/SELECT policies were removed after verification. Post-operation policy count for `pf_one_time_airtable_export_%` is **0**.

## Registry evidence update

The earlier historical Airtable evidence version `2026-09-23` remains preserved but is superseded.

Current recognized evidence version:

- artifact: `pf.artifact.legacy-airtable-registry-export`
- version: `2026-09-24-pre-retirement`
- digest: `sha256:35214d1dae9c79fc05256da00a797f3b0d4c0eca5e00921108502c070b8a36d2`
- size: `537688`
- round-trip verified: true
- Minivault locator recorded in artifact metadata

## Airtable authority retirement

After Minivault custody was verified, all **38 legacy tables** were deleted from the Airtable base.

This includes the old Registry, contract/grant, CAS, research/evidence, census, topology, treasury and other pre-V0 tables.

The legacy Airtable data model is therefore no longer live authority.

## Powerfarm Search projection

A new table named `Powerfarm Search` was created before the old tables were removed.

It is the **only remaining table** in the base.

Current projection:

- table id: `tblvDHGvfaLn3nL9T`
- rows: **15**
- source rows currently projected from Supabase Registry and Minivault
- authority field is explicitly `projection-only`

Fields:

- Object ID
- Source
- Kind
- Title
- Summary
- Version
- Digest
- Status
- Authority

The source vocabulary includes:

- Supabase Registry
- Supabase Minivault
- Apple CloudKit

No Apple app-database rows are projected yet because final contract-owned CloudKit databases/namespaces have not yet been provisioned.

## Airtable shell note

The Airtable connector can delete tables but cannot delete or rename the base itself.

Therefore the historical base shell still carries its old base-level name, while its entire old schema has been destroyed and replaced by the sole `Powerfarm Search` projection table.

This shell is not authority. A future manual/provider-capable operation may rename the base itself to `Powerfarm Search` if desired.

## Supabase security verification

The only current Supabase Security Advisor notices remain the five intentional informational notices that Registry Core tables have RLS enabled with no client policies.

This is expected while Registry mutation remains private.

## Result

The Airtable negative delta is closed at the data-model level:

**38 legacy tables → durable Minivault export → verified custody → deleted → one rebuildable Search projection.**

Airtable is now a projection surface rather than the Registry.
