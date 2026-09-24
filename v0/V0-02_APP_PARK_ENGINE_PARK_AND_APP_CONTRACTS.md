# V0-02 - App Park, Engine Park and App Contracts

**Status:** WORKING V0, recognized at `6438c55a20e82e922322d26561487f91761a6e3a`  
**Scope:** finite V0 runtime and placement contract for the LABs.

## Purpose

PF-03 defines an App Contract as the root institutional contract of an application. This document makes the V0 materialization explicit enough to compute topology and cleanup deltas.

A directory, process, package or database does not become a Powerfarm application merely because it exists on a LAB.

## V0 machine set

The current V0 territory contains these machines:

- `pf.lab-8gb`
- `pf.lab-512`
- `pf.lab-256`

LAB 256 is included in the target set even when observation coverage is temporarily incomplete.

Each machine has four conceptual areas:

```text
protected human/system material
POWERFARM institutional root
App Park <host>
Engine Park <host>
```

Exact filesystem paths are materialization detail and are generated from topology once adopted.

## App Park

An App Park contains admitted Powerfarm applications assigned to that place.

An application belongs in App Park only when an adopted App Contract identifies:

- stable application identity;
- owner/principal;
- source repository and recognized artifact version;
- placement;
- lifecycle state;
- owned state stores and their authority;
- capabilities provided and consumed;
- health/verification interface;
- required Antenna, Heartime, Continuity and Search relationships;
- install, upgrade, retirement and recovery semantics;
- secret references, never secret values.

A repo clone without an App Contract is not an admitted application.

## Engine Park

An Engine Park contains shared execution/runtime engines intentionally provided as place capabilities.

An engine belongs in Engine Park only when Registry recognition and a contract identify:

- stable engine identity;
- supported capability;
- recognized version;
- placement;
- consumers;
- resource requirements;
- verification/health contract;
- upgrade and retirement path.

Language runtimes, model runtimes, browsers, databases or toolchains are not automatically engines. They become engines only when Powerfarm recognizes them as shared capabilities.

## Host Runner

V0 requires one deterministic Host Runner per LAB as the materialization/execution boundary for approved machine-changing operations.

The Host Runner:

- executes allow-listed jobs;
- checks preconditions and protected paths;
- produces receipts;
- reports health;
- does not grant itself authority;
- does not make LLM output equivalent to approval.

Agents may propose. The runner executes only authorized plans.

## Initial V0 application set

The initial target recognizes these logical applications/components, subject to exact manifest expansion in `registry-v0.yaml`:

- `pf.minivault`
- `pf.search`
- `pf.host-runner` on each LAB
- `pf.identity`
- `pf.continuity`
- `pf.antenna`
- `pf.heartime`
- `pf.research`
- operator-facing projection surfaces required by the adopted V0
- the explicitly adopted App Park applications discovered during target compilation

This list is a target namespace, not permission to keep every historical implementation bearing a similar name.

## Placement law

Registry/Ideal Registry declares logical placement. Materialization follows:

```text
recognized app/engine
  -> App Contract / capability contract
  -> topology rule
  -> target Place
  -> materialize
  -> verify
  -> census
  -> recognize/adopt
```

Physical presence never precedes authority logically, even when bootstrap work temporarily creates bytes before final recognition.

## State stores

Application state stores MUST be declared by contract with at least:

- store id;
- engine;
- purpose;
- owner;
- place or remote substrate;
- authoritative_for;
- durability;
- schema/migration identity;
- snapshot/backup rule;
- searchability;
- sensitivity.

SQLite is allowed when appropriate but is not the V0 default authority for every project. CloudKit and Supabase are adopted where their authority scope fits.

## Negative-delta implications

An installed app/engine/process is negative-delta material when it is not required by:

- protected human/system rules;
- an adopted App Contract;
- an adopted Engine capability contract;
- a declared temporary migration exception.

Disposition is explicit: delete, archive-then-delete, keep outside Registry, quarantine/decide, or replace.

## Positive-delta implications

A required V0 application is positive delta until:

1. its Registry identity exists;
2. its recognized artifact/version exists;
3. its App Contract is adopted;
4. its placement is declared;
5. required grants and secret references exist;
6. it is materialized;
7. health/admission evidence passes;
8. the post-materialization census observes it where expected.

## V0 exit criteria

Every App Park and Engine Park resident is explained by an adopted contract, and every adopted contract has a matching verified materialization or an explicit declared exception.
