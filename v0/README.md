# Powerfarm V0

**Status:** WORKING V0  
**Recognition baseline:** Director merge of PR #5, commit `6438c55a20e82e922322d26561487f91761a6e3a`.  
**Purpose:** make Powerfarm finite enough to clean, verify, and then build.

The six Powerfarm research documents remain canon. This package turns that durable doctrine into a finite V0 materialization.

## Architecture in three questions

| Sector | Question | V0 responsibility |
|---|---|---|
| **Research** | **What we study** | Experiments, evidence, techniques, software produced by research, findings and conclusions. |
| **Continuity** | **How we do it** | Materialization and execution: LABs, workflows, App Park, Engine Park, onboarding, verification and recovery. |
| **Identity** | **Who we are** | OAuth/principals, Registry recognition and Minivault preservation. |

Everything else is a service, contract, projection or replaceable substrate supporting those sectors.

The Registry is Powerfarm's institutional skeleton. It records the identities, versions, contracts, grants, templates and relationships that define admissible Powerfarm structure. It does **not** mirror ordinary daily operational state.

Daily work remains with the software that owns it. When that work produces durable institutional value, the valuable object may be promoted into Minivault and recognized by the Registry.

## Finite cleanup model

Let:

- **C** = Current Registry Situation: what Powerfarm currently recognizes or relies on, reconstructed from census and evidence.
- **I** = Ideal Registry V0: the finite state Powerfarm intends to recognize.

Then:

```text
Negative Delta = C - I
Positive Delta = I - C
```

A replacement may appear in both.

Allowed negative-delta dispositions are:

- `DELETE`
- `ARCHIVE_THEN_DELETE`
- `ARCHIVE_THEN_MOVE`
- `KEEP_OUTSIDE_REGISTRY`
- `QUARANTINE_OR_DECIDE`
- `REPLACE`

The Raw Census observes the world. It is evidence for C, not C itself.

## Document ownership

| File | Owns |
|---|---|
| `PF-03_Powerfarm_Operating_System.md` | Durable institutional architecture. |
| `PF-04_Intelligence_and_Technology_System.md` | Durable technical and engineering doctrine. |
| `V0-01_MINIVAULT_STORAGE_AND_REGISTRY.md` | Identity materialization: Registry, Minivault, Supabase, Search/Airtable and repository preservation. |
| `V0-02_APP_PARK_ENGINE_PARK_AND_APP_CONTRACTS.md` | Continuity materialization: LABs, Google ADK workflows, Parks, onboarding and CloudKit provisioning. |
| `V0-03_NAMESPACE_AUTHORITY_AND_SECRETS.md` | Names, principals, grants, secret references and approvals. |
| `V0-04_CURRENT_REGISTRY_SITUATION.md` | C only: current evidence-backed recognition and bounded unknowns. |
| `V0-05_IDEAL_REGISTRY_V0.md` | I only: the finite target and convergence condition. |
| `registry-v0.yaml` | Machine-readable target, dispositions and unresolved gates. |
| `PF-03-PF-04-DECONSTRUCTION.md` | Historical rationale for separating durable canon from V0 materialization. |

PF-01, PF-02, PF-05 and PF-06 are unchanged by this materialization pass.

## Convergence

Cleanup is complete when:

```text
C - I = empty except explicit retained/deferred exceptions
I - C = empty
post-cleanup census matches adopted topology
Current Registry digest = adopted Ideal Registry V0 digest
```

Only after that cleanup convergence does the V0 program move from removing legacy material to building missing positive delta.
