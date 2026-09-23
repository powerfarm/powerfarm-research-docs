# Powerfarm V0 target package

**Status:** PROPOSED  
**Recognition rule:** this package becomes the working V0 definition only when the Director merges its pull request into `main`.  
**Date:** 23 September 2026

This directory exists to make Powerfarm V0 finite before further consolidation work.

The six existing Powerfarm research documents remain the governing canon. This package does not replace their durable doctrine. It makes the current V0 materialization explicit enough to compute the difference between what exists and what should exist.

## The finite model

Let:

- **C** = Current Registry Situation, reconstructed from the frozen Census and recognized live sources.
- **I** = Ideal Registry V0, the finite set of entities, artifacts, contracts, grants, stores and placements Powerfarm intends to recognize for V0.

Then:

- **Negative Delta = C - I**: current recognized/materialized things that do not belong in V0.
- **Positive Delta = I - C**: V0 requirements that are missing or not yet recognized.
- A replacement may appear in both deltas: retire the old instance and build/recognize the new one.

A negative-delta item is not automatically deletion. Its disposition is one of:

- `DELETE`
- `ARCHIVE_THEN_DELETE`
- `KEEP_OUTSIDE_REGISTRY`
- `QUARANTINE_OR_DECIDE`
- `REPLACE`

## Files

1. `V0-01_MINIVAULT_STORAGE_AND_REGISTRY.md`  
   Minivault semantics; Supabase company/control plane; CloudKit LAB-adjacent project-vault plane; content storage; Search; Airtable projection.

2. `V0-02_APP_PARK_ENGINE_PARK_AND_APP_CONTRACTS.md`  
   V0 runtime shape on the LABs: App Parks, Engine Parks, Host Runner, placement and App Contract materialization.

3. `V0-03_NAMESPACE_AUTHORITY_AND_SECRETS.md`  
   PFID/namespace rules, principals, grants, authority boundaries, machine identities and secret references. No secret value belongs in this public repository.

4. `V0-04_CURRENT_REGISTRY_SITUATION.md`  
   Inputs and reconstruction rules for C. This is a finite recognition view, not a dump of every filesystem byte.

5. `V0-05_IDEAL_REGISTRY_V0.md`  
   Human-readable target I and admission rules.

6. `registry-v0.yaml`  
   Machine-readable initial V0 manifest. This file is intended to become the comparison input for delta computation.

7. `PF-03-PF-04-DECONSTRUCTION.md`  
   Separates durable architectural law from older materialization choices in PF-03 and PF-04 before those canonical documents are revised.

## Existing canon treatment

For this pass:

- **PF-01 Powerfarm Charter:** unchanged.
- **PF-02 Research and Evidence Standard:** unchanged.
- **PF-05 Products and Business System:** unchanged.
- **PF-06 Standard Documents Catalog:** unchanged.
- **PF-03 Powerfarm Operating System:** deconstruct materialization-specific clauses; preserve durable architectural doctrine.
- **PF-04 Intelligence and Technology System:** deconstruct implementation/materialization-specific clauses; preserve representation, verification, replaceability and engineering doctrine.

## Relationship to execution

The 32-step execution sequence remains the implementation program, but it is subordinate to this finite target. Cleanup should increasingly be generated from the deltas rather than discovered ad hoc.

The convergence condition is:

```text
Negative Delta = empty, except explicit retained/deferred exceptions
Positive Delta = empty
Current Registry = adopted Ideal Registry V0
```
