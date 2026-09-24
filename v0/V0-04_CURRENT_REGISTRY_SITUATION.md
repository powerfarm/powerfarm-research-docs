# V0-04 - Current Registry Situation

**Status:** WORKING reconstruction of C, V0 package recognized at `6438c55a20e82e922322d26561487f91761a6e3a`  
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

This base is evidence and design input. It is not the adopted V0 authority.

Its terminal V0 disposition is **`DELETE` after verified migration**: authoritative Registry facts are moved/recognized in Supabase, migration receipts are checked, then the old Airtable Registry tables/records are deleted and the Airtable surface is rebuilt as Powerfarm Search. The frozen export, not the live legacy tables, preserves the historical state.

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

A read-only signed census was executed locally on LAB 256 against both CloudKit environments.

**Production**

- account status: available;
- none of the 13 expected Powerfarm record types exist.

**Development**

- account status: available;
- record types proven present: `PFPrincipal`, `PFGrant`, `PFContract`, `PFContent`, `PFHead`;
- record types proven absent: `PFEntity`, `PFPlace`, `PFArtifact`, `PFArtifactVersion`, `PFApplication`, `PFRecognition`, `PFBinding`, `PFSoftware`;
- the surviving Development record families cannot be generically enumerated by the historical `TRUEPREDICATE` code path because the required query index is absent.

Therefore the earlier apparent zero counts are **not** treated as proof that Development is empty. Population of the five surviving record families remains to be recovered by deterministic record IDs / direct fetch before **CK-LIVE-001** is closed.

These surviving Development records are understood to be **old test material**. Their terminal V0 disposition is **`DELETE`** after the census proves their exact population and any still-useful payload is migrated or shown to be unnecessary. They are not a legacy Registry to preserve in CloudKit.

The later Apple transition plan proposed a Private custom zone, historically named `PowerfarmInstitution`, but that zone has **not yet been proven live** in this reconstruction.

### 6. Supabase

A live Powerfarm Supabase project is directly observed through the provider connector:

- project ref: `ekjlmclhqnsstfjzuabz`;
- provider-side name: `powerfarm.kernal`;
- region: `eu-west-1`;
- state: `ACTIVE_HEALTHY`;
- PostgreSQL: 17.6.1.166 / engine 17;
- user migrations: 0;
- Storage buckets: 0;
- Edge Functions: 0;
- Auth users: 0;
- development branches: 0;
- Supabase Vault exists and is empty;
- only platform/system schemas and tables were observed.

This resolves **SUPABASE-LIVE-001**. The project is a clean, unmaterialized current substrate rather than a legacy Powerfarm database. Working V0 binds it to institutional identity `pf.store.supabase.company`; the provider-side spelling does not define that identity.

### 7. Powerfarm Search and Airtable projection

Powerfarm Search exists as architectural doctrine/design but no complete federated Supabase + CloudKit Search implementation has yet been proven live.

Airtable currently exists as benchmark/design state, not yet as the rebuildable projection of Powerfarm Search specified by V0.

### 8. GitHub repository territories

The active Powerfarm GitHub organization currently exposes at least these observed repositories:

- `powerfarm/.github`
- `powerfarm/powerfarm-identity`
- `powerfarm/powerfarm-antenna`
- `powerfarm/powerfarm-specs`
- `powerfarm/powerfarm-process-manager`
- `powerfarm/powerfarm-coloured-places`
- `powerfarm/powerfarm-continuity`
- `powerfarm/powerfarm-platform`
- `powerfarm/powerfarm-research-docs`
- `powerfarm/powerfarm-cli`
- `powerfarm/powerfarm-heartime`

Observation is not adoption. **REPO-CURRENT-001** remains open until each observed repository receives an explicit V0 disposition.

A separate GitHub organization, **`powercitty`**, is designated by the Director as the historical-preservation destination for superseded repositories. Moving a repository from Powerfarm to `powercitty` means **archive/preserve outside the active Registry**, not deletion.

The GitHub App is installed on `powercitty`. A live provider census on 23 September 2026 observed **18 repositories with mixed public/private visibility**. The detailed repository-name inventory is retained in private LAB receipts rather than repeated in this public canon.

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
3. **APP-PARK-CURRENT-001:** enumerate currently recognized App Park residents versus mere directories/processes.
4. **ENGINE-PARK-CURRENT-001:** enumerate currently recognized Engine Park residents versus installed tools/runtimes.
5. **SECRET-REFS-001:** enumerate required secret references by stable name/consumer without capturing values.
6. **REPO-CURRENT-001:** classify observed Powerfarm repositories as V0-survivor, historical-preserved, or outside Registry scope.

There is no open-ended discovery clause beyond these categories. New facts found while resolving them are entered under one of these categories or require an explicit amendment to this document.

## Freeze condition for C

Current Registry Situation is frozen when:

- every unresolved item above is resolved or explicitly marked unavailable with bounded impact;
- every C row has a source/provenance reference;
- current identities are stable enough to compare against `registry-v0.yaml`;
- C has a canonical digest.

Only then should the full negative and positive deltas be treated as authoritative cleanup/build lists.
