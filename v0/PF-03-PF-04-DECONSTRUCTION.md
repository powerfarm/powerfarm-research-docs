# PF-03 / PF-04 Deconstruction for V0

**Status:** WORKING V0, recognized at `6438c55a20e82e922322d26561487f91761a6e3a`  
**Date:** 23 September 2026

## Why this exists

Powerfarm's architectural spirit has remained comparatively stable while its materialization changed repeatedly.

The purpose of this pass is therefore **not** to replace the architecture. It is to separate:

1. durable institutional/technical law that belongs in PF-03/PF-04; from
2. current V0 substrate choices that belong in the `v0/` materialization specifications.

This allows implementations to change without creating the impression that Powerfarm's identity changes every time storage, cloud or LAB topology changes.

## Files intentionally untouched

This pass makes no content changes to:

- PF-01 Powerfarm Charter;
- PF-02 Research and Evidence Standard;
- PF-05 Products and Business System;
- PF-06 Standard Documents Catalog.

Their public, research and product/business doctrine remains as currently adopted.

## PF-03: durable spine to preserve

The following remain canonical architecture:

- Research / Continuity / Identity as durable sectors;
- Registry as a service of institutional recognition, not omniscient operational truth;
- **state is local, contracts are global**;
- authority is explicit;
- execution is causal;
- preserved exact bytes may be immutable/content-addressed;
- context is a working set, not a warehouse;
- provenance accompanies important assertions;
- source control, immutable content, Registry recognition and mutable operational state are distinct homes;
- App Contract as root application contract;
- declared state-store ownership and authority;
- Declare -> Materialize -> Prove -> Recognize;
- Antenna / Heartime / Continuity responsibility boundaries;
- Search as federated read model/projection, not authority;
- census as observation against expected population;
- software as temporal trajectory;
- architecture freeze / build-thin discipline.

## PF-03: materialization to extract

### SQLite default

Old canon said:

> SQLite is the default for application-local Powerfarm state unless another mechanism is materially justified.

That statement is a historical materialization choice. The durable rule is the sentence that already followed it:

> The architectural rule is ownership, not SQLite itself.

V0 therefore removes SQLite as a canonical default. SQLite remains permitted where an App Contract demonstrates that it fits local transactional/runtime state.

Current choices such as Supabase, CloudKit and local stores live in `v0/V0-01_MINIVAULT_STORAGE_AND_REGISTRY.md`.

### Legacy Supabase reduction

PF-03's implementation-order text referred to "legacy Supabase reduction". That is an implementation-era phrase and does not belong in durable canon.

The V0 wording instead points concrete materialization work to versioned V0 architecture specifications.

### Parks

App Park and Engine Park remain useful topology/materialization concepts, but their exact residents and paths belong in V0 topology/contracts rather than canonical doctrine.

PF-03 keeps the law that physical presence does not create institutional membership.

## PF-04: durable spine to preserve

PF-04 is already substantially materialization-independent. Preserve:

- semantics rise before implementation;
- executable graph semantics without mandating a graph database/DSL;
- immutable content references;
- context as working set;
- small deliberate production language set;
- language profiles;
- code editorial standard;
- semantic change + verification chain;
- independent verification where consequence justifies it;
- Evidence Fabric;
- replaceability and external leverage;
- build thin;
- evidence-driven intelligence routing;
- security/data baseline;
- technology surveillance;
- **current implementation is not canon**;
- replacement rule.

## PF-04: V0 clarification

The only V0 deconstruction needed now is to make explicit that current storage/provider/topology decisions are standard architecture/materialization instances under `v0/`.

Changing those files does not change PF-04 unless representation, verification, authority, replaceability or other durable doctrine changes.

## Deconstruction rule going forward

When reviewing PF-03/PF-04, ask:

> Would this sentence still be true if Supabase, CloudKit, a LAB, a programming language or a provider were replaced?

- If **yes**, it may belong in canon.
- If **no**, it probably belongs in a V0 materialization spec, App Contract, decision record, runbook or other standard instance.

This rule is intentionally biased toward a small stable canon and explicit replaceable materializations.
