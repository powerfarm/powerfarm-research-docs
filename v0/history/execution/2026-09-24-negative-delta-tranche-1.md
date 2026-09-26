# Negative Delta Execution — Tranche 1

**Date:** 24 September 2026  
**Authority:** Director merge of PR #8, commit `d4f748b2212cb827fb90669475351d1d11506cca`  
**Scope:** first destructive execution against the frozen C → I delta.

## LAB filesystem cleanup

### LAB 8GB

Removed:

- `~/App Park/cockpit`
- `~/App Park/work-graph`
- `~/App Park/zelador`
- `~/App Park/zelador-grid`
- `~/Engine Park/live/powerfarm`
- `~/Engine Park/live/workflow-engine`

Pre-delete receipt SHA-256:

`e362910c90c2155135889f6a98c4a57abc10cfc07b5243faa6196edcf80eae94`

### LAB 512

Removed:

- `~/App Park/zelador`

Pre-delete receipt SHA-256:

`06ac005890c70bd6685135df2e39f600540a1c581066cda46a8b9efbc6769ec4`

## Runtime cleanup

Removed obsolete launch agents/runtime trees for:

- legacy MCP portal/tunnel material;
- legacy capacity Registry;
- Eon Fusion runtime services;
- legacy Heartime/ingress runtime;
- Zelador runtime material.

LAB 8GB runtime receipt SHA-256:

`a4595455702b5fed136c83ff62adf7c6de573335e3fe0fa409bb63a450179677`

LAB 512 runtime receipt SHA-256:

`eec62e69ff41b07728809e54230771668bb6a7cdf5fcdb4d91373dddbfe51dd9`

Receipt files are retained locally under:

`~/POWERFARM/.receipts/negative-delta-20260924/`

No live credential values were copied into the execution ledger.

## Protected survivors verified after deletion

### LAB 8GB

- Manhattan daemon: running
- Manhattan agent: running
- Coloured Places launch service `com.minilab.app.places`: loaded
- `~/App Park/coloured-places`: present

### LAB 512

- Manhattan daemon: running
- Manhattan agent: running

No obsolete Powerfarm/Eon/Heartime/Zelador process from this tranche remained after verification.

## GitHub historical-preservation moves

Transferred from `powerfarm` to `powercitty` and archived:

- `powerfarm-process-manager`
- `powerfarm-platform`
- `powerfarm-cli`

GitHub redirects from the old `powerfarm/... ` names resolve to the archived `powercitty/... ` repositories.

Pre-transfer metadata receipt SHA-256 values:

- `powerfarm-process-manager`: `d178edfa19fc61e6dea6d047f6a9837d6dc56dd5dabc002048a3461fb23451c5`
- `powerfarm-platform`: `60256b476f0ebd49e754b573207ff6c065893a19dd44e0bd47f2e685b9933aba`
- `powerfarm-cli`: `2ecb0950bf81a872d9c21807a1d10828382811dbb488930b51fdaeb2268c13e4`

## Provider work still pending

### Supabase

Target deletion remains:

- `Google ADK mapping`
- project ref `vbgzdqdlarulpfsyjrke`

The available Supabase CLI on LAB 8GB is authenticated to a different Supabase account than the connected provider surface owning this project. No deletion was attempted through the mismatched account.

### CloudKit

Historical test data/schema remains scheduled for reset/delete while preserving or recreating Apple provisioning capability. No destructive CloudKit operation was performed in this tranche.

### Airtable / Identity migration

Legacy Airtable Registry retirement remains blocked on the minimal Identity/Registry migration bridge into `powerfarm.kernal`.

## Result

This tranche removes the first obvious machine/runtime/repository negative delta while preserving the explicitly recognized survivors.

The cleanup program remains in **Negative Delta execution**, not Positive Delta build.
