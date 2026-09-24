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

The surviving Development state is classified by the Director as disposable test material. Exact record-by-record enumeration no longer blocks cleanup. The signed census/receipts preserve the evidence boundary; historical CloudKit data/schema may be wiped and rebuilt while preserving the Apple developer/container capability.

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

The same live provider census currently exposes one additional project, `Google ADK mapping` (project ref `vbgzdqdlarulpfsyjrke`). Read-only inspection found no user tables, no Auth users, no Storage buckets, no user migrations, no Edge Functions and no development branches. It has no role in I and is negative delta with target disposition `DELETE` after recognition of this target and dependency verification.

### Legacy Supabase Identity/Registry source

A historical Supabase implementation named `powerfarm-registry` contains prior OAuth/Registry-era material.

It is **not** the V0 destination and must not be modernized in place.

The current connected Supabase account does not expose a live project by that name. The historical source is, however, preserved locally on LAB 8GB at `~/lab/powerfarm-registry` with migrations covering identities/identity links, artifacts/versions/relations, grants, approvals, OAuth clients, service definitions/contracts/events, runs, ADK runtime state, workspaces and gadget state.

This bounds the migration problem:

- Identity/Registry concepts and any still-required recognized facts are migration input;
- old runs, ADK session/event/checkpoint/effect state, workspace/gadget drafts and other operational implementation state do not migrate merely because the old schema contained them;
- the frozen Airtable export and local migration/source history provide the remaining reconstruction evidence if the old cloud project is no longer available.

No live legacy Supabase authority is currently visible through the provider connection.

### Continuity survivor observations

Live inspection on 24 September 2026 established:

- Manhattan daemon + agent are running on **both** ecosystem LABs and are protected survivors.
- Coloured Places exists under LAB 8GB App Park with a built Next.js application and admission documentation, but no live Coloured Places process was observed.
- Google ADK was not found installed on either ecosystem LAB.
- LAB 8GB App Park contains `coloured-places`, `work-graph`, `zelador`, `zelador-grid`, plus `cockpit` as a symlink to an older UI.
- LAB 512 App Park contains `zelador`.
- LAB 8GB Engine Park contains `powerfarm` and `workflow-engine`; LAB 512 Engine Park has no live resident.
- `~/POWERFARM` currently contains receipts but no canonical Research workspace, making `~/POWERFARM/Research` a clean positive-delta target.

Director disposition resolves the Park census:

- `coloured-places`: **KEEP / REPAIR / ADMIT**;
- Manhattan on both LABs: **KEEP / PROTECT**;
- LAB 8GB `work-graph`, `zelador`, `zelador-grid`, `cockpit`: **DELETE**;
- LAB 512 `zelador`: **DELETE**;
- LAB 8GB Engine Park `powerfarm` and `workflow-engine`: **DELETE**;
- Google ADK: **positive delta**, to become the required Engine Park resident.

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

The current repository classification is:

**Active V0 source territory**

- `powerfarm/.github` — organization metadata/configuration; retained outside software authority.
- `powerfarm/powerfarm-research-docs` — canon and V0 target.
- `powerfarm/powerfarm-specs` — operational contracts/specifications.
- `powerfarm/powerfarm-identity` — active Identity source; its older Registry/ADK/workspace implementation details do not automatically survive the V0 migration.
- `powerfarm/powerfarm-continuity` — active Continuity source; machine materialization must converge on the Google ADK/Host Runner/Park model.
- `powerfarm/powerfarm-coloured-places` — required Continuity observability/urgent-fix app.
- `powerfarm/powerfarm-antenna` — retained source for the PF-03 Antenna service responsibility; not automatically an admitted runtime.
- `powerfarm/powerfarm-heartime` — retained source for the PF-03 Heartime service responsibility; not automatically an admitted runtime.

**Historical-preservation disposition**

- `powerfarm/powerfarm-process-manager` → `ARCHIVE_THEN_MOVE` to `powercitty`.
- `powerfarm/powerfarm-platform` → `ARCHIVE_THEN_MOVE` to `powercitty`.
- `powerfarm/powerfarm-cli` → `ARCHIVE_THEN_MOVE` to `powercitty`.

GitHub organization `powercitty` is the historical-preservation territory for superseded repositories. A live census observed 18 repositories there with mixed visibility. Detailed names remain in private receipts.

Moving a repo from `powerfarm` to `powercitty` preserves source/history but ends active V0 Registry membership.

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

## C freeze readiness

All previously bounded census gates are now resolved or explicitly bounded:

- CloudKit historical test state is disposable under Director decision; signed census evidence is sufficient.
- LAB 256 is outside ecosystem expected population.
- App Park and Engine Park residents have explicit keep/delete/add dispositions.
- required secret references are bounded by name/consumer without values.
- observed Powerfarm repositories have explicit active or historical-preservation disposition.
- no live `powerfarm-registry` project is visible through the connected Supabase account; local migrations/source plus frozen institutional exports bound the recoverable migration evidence.

**No open census category remains before C freeze.**

Director merge of this target can serve as the recognition point after which C is frozen and the negative delta becomes executable.

There is no open-ended discovery clause. New facts must fit one of these gates or explicitly amend C.

## Freeze condition

C freezes when every gate is resolved or explicitly bounded, every row has provenance, identities are stable enough for comparison with `registry-v0.yaml`, and C has a canonical digest.
