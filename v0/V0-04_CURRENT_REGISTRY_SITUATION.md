# V0-04 - Current Registry Situation

**Status:** WORKING reconstruction of C  
**Recognition baseline:** `6438c55a20e82e922322d26561487f91761a6e3a`  
**As-of:** 24 September 2026

**C** is the finite set of institutional state Powerfarm currently recognizes or relies on. It is reconstructed from evidence; it is not the Raw Census.

Unknowns remain unknown until resolved. Observation alone does not admit a thing into Powerfarm.

## Evidence boundary

C currently draws from:

- September census and cleanup receipts;
- frozen Airtable export;
- frozen local `.powerfarm` CAS/manifests/certifications/capacities;
- LAB material/process/topology observations;
- Apple/CloudKit implementation and signed census;
- Supabase provider observations;
- GitHub repositories and preservation territory;
- research canon and execution receipts.

## Current recognized / relied-on sources

### Canon

PF-01 through PF-06 are the recognized research/governance canon. PF-03/PF-04 contain the durable architecture/technical doctrine that V0 materializes.

### Airtable legacy Registry

Frozen benchmark export:

- base: `Powerfarm - LLM Engineering Benchmark Powerplant`
- 38 tables
- 347 records
- SHA-256: `0ea09c53bc59512118c69f60f7572d19ae2e48c0cbf23bf183c033bd2863e9ec`

It contains Registry-shaped research, artifact, contract, authority, topology and census state.

It is a **migration source**, not V0 authority. Required institutional truth moves to Supabase Identity; after verification, the old Registry tables/records are deleted. The frozen export and migration receipts preserve history.

### Local Registry/CAS evidence

Frozen verified CAS:

- LAB 8GB: 62 objects, 0 mismatches;
- LAB 512: 66 objects, 0 mismatches.

Associated manifests, certifications and capacities remain evidence to reconcile into C. Their mere presence does not imply V0 admission.

### Machines

Current ecosystem machine population:

- `pf.lab-8gb`: online, headless/always-on target.
- `pf.lab-512`: online, headless/always-on target.

LAB 256 is the Director's personal/mobile computer and is **outside the ecosystem**. Its intermittent availability is expected, not a health failure. Historical Powerfarm material on LAB 256 is evidence/migration input only; no V0 service may depend on it.

### CloudKit legacy test state

Container: `iCloud.app.powerfarm`.

Historical Apple code used the Public Cloud Database with record families:

`PFEntity`, `PFPrincipal`, `PFGrant`, `PFPlace`, `PFContract`, `PFArtifact`, `PFArtifactVersion`, `PFApplication`, `PFRecognition`, `PFBinding`, `PFSoftware`, `PFContent`, `PFHead`.

Signed census established:

- **Production:** none of the 13 historical record types exist.
- **Development present:** `PFPrincipal`, `PFGrant`, `PFContract`, `PFContent`, `PFHead`.
- **Development absent:** the other eight expected types.
- generic historical `TRUEPREDICATE` enumeration fails because the required query index is absent.

The exact surviving Development population is still unresolved. These records are old test material with terminal disposition `DELETE` after exact enumeration and migration of anything uniquely required.

The previously proposed `PowerfarmInstitution` private zone is historical design input, not a proven V0 resource.

### Supabase Identity destination

Observed destination:

- institutional binding: `pf.store.supabase.company`
- project ref: `ekjlmclhqnsstfjzuabz`
- provider name: `powerfarm.kernal`
- region: `eu-west-1`
- state: `ACTIVE_HEALTHY`
- PostgreSQL 17.6.1.166 / engine 17

At first census it had:

- 0 user migrations;
- 0 Storage buckets;
- 0 Edge Functions;
- 0 Auth users;
- 0 development branches;
- empty Supabase Vault;
- only platform/system tables.

It is therefore treated as the clean V0 Identity destination whose schema/kernel is still to be built.

### Legacy Supabase Identity/Registry source

A separate historical Supabase project named `powerfarm-registry` contains prior OAuth/Registry-era material.

It is **not** the V0 destination and must not be modernized in place.

Its exact contents have not yet been provider-censused for this V0 reconstruction. Required institutional truth must be identified, migrated into the V0 Identity destination, verified, and the legacy project then retired/disregarded as authority.

### Continuity survivor observations

Live inspection on 24 September 2026 established:

- Manhattan daemon + agent are running on **both** ecosystem LABs and are protected survivors.
- Coloured Places exists under LAB 8GB App Park with a built Next.js application and admission documentation, but no live Coloured Places process was observed.
- Google ADK was not found installed on either ecosystem LAB.
- LAB 8GB contains several current/historical App Park residents beyond Coloured Places, including `zelador-grid`, `work-graph`, `cockpit` and `zelador`.
- LAB 512 App Park contains `zelador`.
- Engine Park contains historical/current workflow-engine and Powerfarm trees that are not yet admitted by the simplified V0 target.
- `~/POWERFARM` currently contains receipts but no canonical Research workspace, making `~/POWERFARM/Research` a clean positive-delta target.

These observations substantially bound APP-PARK-CURRENT-001 and ENGINE-PARK-CURRENT-001: unexplained Park residents are candidate negative delta until explicitly contracted.

### Search / Airtable projection

Powerfarm Search exists as architecture/design; a complete federated implementation has not yet been proven live.

Airtable is not yet the rebuildable Search frontend required by I.

### GitHub territories

Observed active/candidate Powerfarm repositories include:

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

Observation is not adoption.

GitHub organization `powercitty` is the historical-preservation territory for superseded repositories. A live census observed 18 repositories there with mixed visibility. Detailed names remain in private receipts.

Moving a repo from `powerfarm` to `powercitty` is `ARCHIVE_THEN_MOVE`, not active V0 membership.

## Fragmentation to reconcile

Current institutional meaning is spread across:

```text
canon
Airtable legacy Registry
local CAS/manifests
legacy Supabase Registry/OAuth
CloudKit test state
LAB material state
GitHub history
execution receipts
```

V0 reconciles these sources with provenance rather than declaring any one retrospectively complete.

## Bounded unresolved gates before C freezes

1. **CK-LIVE-001**: enumerate exact surviving CloudKit Development records/assets/heads.
2. **APP-PARK-CURRENT-001**: distinguish admitted App Park residents from mere directories/processes.
4. **ENGINE-PARK-CURRENT-001**: distinguish admitted Engine Park residents from installed runtimes/tools.
5. **SECRET-REFS-001**: enumerate stable secret references/consumers without values.
6. **REPO-CURRENT-001**: classify observed Powerfarm repos as V0 survivor, historical-preserved or outside scope.
7. **LEGACY-SUPABASE-001**: census `powerfarm-registry`, identify required OAuth/Registry/Minivault truth, and produce the migration set.

There is no open-ended discovery clause. New facts must fit one of these gates or explicitly amend C.

## Freeze condition

C freezes when every gate is resolved or explicitly bounded, every row has provenance, identities are stable enough for comparison with `registry-v0.yaml`, and C has a canonical digest.
