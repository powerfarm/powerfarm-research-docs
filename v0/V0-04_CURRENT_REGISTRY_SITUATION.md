# V0-04 - Current Registry Situation

**Status:** PROPOSED reconstruction of C  
**As-of:** 23 September 2026  
**Purpose:** define the finite current recognition situation used for delta calculation.

This is not the Raw Census itself. The Census observes what exists. **Current Registry Situation (C)** records what Powerfarm currently recognizes or is relying on as institutional state, including fragmented legacy recognition that has not yet been consolidated.

## Evidence boundary

The initial reconstruction uses:

- frozen September 22 Raw Census and post-census receipts;
- frozen Airtable benchmark export;
- `.powerfarm` CAS/manifests/certifications/capacities on LAB 8GB and LAB 512;
- live host/process/topology observations made during consolidation;
- the existing Apple/CloudKit implementation on LAB 256;
- the six research documents in this repository;
- GitHub repository identity where explicitly adopted;
- current execution receipts.

Unknown live data is recorded as unknown, not guessed.

## Current recognition sources

### 1. Research canon

Currently recognized canonical research/governance documents:

- PF-01 Powerfarm Charter
- PF-02 Research and Evidence Standard
- PF-03 Powerfarm Operating System
- PF-04 Intelligence and Technology System
- PF-05 Products and Business System
- PF-06 Standard Documents Catalog

PF-03/PF-04 contain durable doctrine plus some materialization choices now being deconstructed.

### 2. Airtable benchmark Registry

A frozen export exists for the benchmark base:

- base: `Powerfarm - LLM Engineering Benchmark Powerplant`
- 38 tables
- 347 records
- export SHA-256: `0ea09c53bc59512118c69f60f7572d19ae2e48c0cbf23bf183c033bd2863e9ec`

The base contains an extensive Registry-like schema including principles, operators, models, technologies, benchmarks, claims, experiments, artifacts, registry items/relations, contracts, capacities, permissions, grants, territories, topology rules, censuses and census observations.

This base is evidence and design input. It is not yet the adopted V0 authority.

### 3. Powerfarm local Registry/CAS state

Verified frozen CAS state:

- LAB 8GB: 62 CAS objects, 0 hash mismatches.
- LAB 512: 66 CAS objects, 0 hash mismatches.

Associated `.powerfarm` manifests, certifications, capacities and Capacity Registry material were frozen during A1.

These bytes and records are current evidence. Individual items still need reconciliation into C and then comparison with I.

### 4. Machines

Current V0 machine population:

- `pf.lab-8gb` - active and remotely managed.
- `pf.lab-512` - active and remotely managed.
- `pf.lab-256` - reachable over SSH; Desktop Commander agent observed offline during this reconstruction.

The Raw Census and subsequent cleanup receipts define their current material state. Machine presence alone does not admit every installed artifact.

### 5. Apple/CloudKit implementation

On LAB 256, the historical Apple implementation exists under `Powerfarm-apple-native`.

Verified implementation facts:

- CloudKit container identifier: `iCloud.app.powerfarm`.
- current Swift Registry adapter selects `publicCloudDatabase`;
- current Content Store uses Public Cloud Database `PFContent` + `CKAsset`;
- content records use SHA-256 digest-based record names;
- record vocabulary includes PFEntity, PFPrincipal, PFGrant, PFPlace, PFContract, PFArtifact, PFArtifactVersion, PFApplication, PFRecognition, PFBinding, PFSoftware, PFContent and PFHead.

The later Apple transition plan proposed a Private custom zone, historically named `PowerfarmInstitution`, but that zone has **not yet been proven live** in this reconstruction.

Live CloudKit record population is an explicit current unknown because non-interactive `cktool` access cannot unlock the developer credential. This must be enumerated through an interactive Apple-authenticated session before C is frozen.

### 6. Supabase

Supabase is the selected V0 company/control-plane direction, but no Supabase project has yet been adopted as the authoritative Current Registry in this reconstruction.

Therefore:

- Supabase target design belongs in I;
- any existing Supabase resources discovered later must be reconciled into C before adoption;
- presence of credentials does not prove adopted infrastructure.

### 7. Powerfarm Search and Airtable projection

Powerfarm Search exists as architectural doctrine/design but no complete federated Supabase + CloudKit Search implementation has yet been proven live.

Airtable currently exists as benchmark/design state, not yet as the rebuildable projection of Powerfarm Search specified by V0.

## Current fragmentation

Today, institutional recognition is fragmented across:

```text
research canon
Airtable benchmark Registry
.powerfarm manifests/certifications/CAS
Apple CloudKit implementation
LAB material state
GitHub repositories/history
execution receipts
```

The V0 program does not declare one of these retrospectively omniscient. It reconciles them into C with provenance.

## Finite unresolved items before C is frozen

The following unknowns must resolve to an explicit finite record or explicit absence:

1. **CK-LIVE-001:** enumerate live records/assets/heads in `iCloud.app.powerfarm` by environment/database/zone.
2. **LAB256-CENSUS-001:** reconcile the LAB 256 current material census to the same population granularity used for the other LABs.
3. **SUPABASE-LIVE-001:** determine whether any existing Powerfarm Supabase project/resources must be recognized as current state or treated as unadopted experiments.
4. **APP-PARK-CURRENT-001:** enumerate currently recognized App Park residents versus mere directories/processes.
5. **ENGINE-PARK-CURRENT-001:** enumerate currently recognized Engine Park residents versus installed tools/runtimes.
6. **SECRET-REFS-001:** enumerate required secret references by stable name/consumer without capturing values.
7. **REPO-CURRENT-001:** enumerate GitHub repositories that are institutionally recognized today versus historical/experimental repos.

There is no open-ended discovery clause beyond these categories. New facts found while resolving them are entered under one of these categories or require an explicit amendment to this document.

## Freeze condition for C

Current Registry Situation is frozen when:

- every unresolved item above is resolved or explicitly marked unavailable with bounded impact;
- every C row has a source/provenance reference;
- current identities are stable enough to compare against `registry-v0.yaml`;
- C has a canonical digest.

Only then should the full negative and positive deltas be treated as authoritative cleanup/build lists.
