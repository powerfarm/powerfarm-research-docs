# PF-03 / PF-04 Deconstruction for V0

**Status:** WORKING V0  
**Recognition baseline:** `6438c55a20e82e922322d26561487f91761a6e3a`

## Purpose

This note records the boundary used when V0 separated durable canon from replaceable materialization.

It is intentionally short. PF-03 and PF-04 themselves are the authoritative homes for the doctrine; this file does not duplicate their contents.

PF-01, PF-02, PF-05 and PF-06 are unchanged by this pass.

## Boundary

**PF-03 owns durable institutional architecture**, including the three sectors, explicit authority, contracts, Registry/Identity semantics, causal execution, application-owned state, Search/census boundaries and the rule that physical presence does not create institutional membership.

**PF-04 owns durable technical doctrine**, including representation, verification, language/toolchain policy, Evidence Fabric, replaceability, security baseline and build-thin discipline.

**V0 materialization specifications own current choices**, including:

- providers and accounts;
- database/storage engines;
- LAB topology and Park residents;
- concrete paths and locators;
- current migrations/retirements;
- implementation-specific onboarding and execution machinery.

## Historical choices extracted from canon

Two earlier implementation-era choices were deliberately removed from durable canon:

1. **SQLite as the default application-local store.**  
   Durable rule: state belongs to its owning application under declared authority. SQLite remains allowed when a contract selects it.

2. **"Legacy Supabase reduction" as implementation order.**  
   Durable rule: materialization work belongs in versioned specifications and contracts, not permanent canon.

App Park and Engine Park remain valid topology concepts, but their exact residents, paths and current implementation belong in V0-02 and the Registry target.

## Test

When reviewing PF-03/PF-04, ask:

> Would this statement remain true if Supabase, CloudKit, Google ADK, a LAB, a programming language or another provider were replaced?

- **Yes:** it may belong in canon.
- **No:** it belongs in a materialization spec, contract, decision record, runbook or other standard instance.

The bias is deliberate: **small stable canon, explicit replaceable materialization.**
