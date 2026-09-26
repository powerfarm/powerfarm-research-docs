# V0-02 - Continuity, Parks and App Contracts

**Status:** WORKING V0  
**Recognition baseline:** `6438c55a20e82e922322d26561487f91761a6e3a`  
**Scope:** V0 materialization of Powerfarm Continuity.

## Continuity

Continuity answers:

> **How do we do it?**

It turns recognized contracts into verified material reality.

Current V0 materialization consists of:

- two always-on macOS LABs: `pf.lab-8gb` and `pf.lab-512`;
- one agent per LAB (§Agents);
- Google ADK Workflow Engine;
- App Park;
- Engine Park;
- onboarding/materialization workflows;
- Host Runner boundaries for machine-changing effects;
- verification, receipts and recovery;
- CloudKit provisioning for contract-declared app/engine databases.

These are current materializations of Continuity, not eternal provider choices.

## V0 machine set

The trusted V0 ecosystem territory contains only:

- `pf.lab-8gb`
- `pf.lab-512`

Both are expected to be continuously available, headless and UPS-backed.

LAB 256 is the Director's personal/mobile computer. It is explicitly **outside the ecosystem expected population** and MUST NOT be required for availability, scheduling, census health, execution, storage or recovery.

Each ecosystem LAB converges to:

```text
protected human/system material
POWERFARM institutional root
App Park
Engine Park
Host Runner
```

Exact filesystem paths are materialization detail.

## Fixed Continuity residents

The following residents are explicit V0 survivors/targets:

- `pf.app.coloured-places`: Continuity observability and urgent-fix/operator application. It runs on Vercel as a projection over the Registry and the Antenna store, not as an App Park resident.
- `pf.process.manhattan`: permanent infrastructure process. Current daemon/agent materializations on both ecosystem LABs are protected from cleanup.
- Google ADK Workflow Engine: required Engine Park resident for Continuity workflows and onboarding. It is currently missing from both ecosystem LABs and is therefore positive delta.

Other current Park residents remain unadmitted until a V0 contract explicitly preserves them.

## Research workspace

Powerfarm Research receives one canonical macOS filesystem root:

`~/POWERFARM/Research`

Research experiments run beneath this root rather than creating durable institutional meaning through arbitrary historical project folders.

Research observability is externalized to **Braintrust**. Braintrust is a Research observability/evaluation surface, not Registry authority.

Historical Research directories outside the canonical root are migration/cleanup candidates: preserve or promote required outputs, then remove or archive them according to the delta.

## App Park and Engine Park

**App Park** contains admitted Powerfarm applications assigned to a LAB.

**Engine Park** contains admitted shared execution/runtime engines provided as place capabilities.

Physical presence does not create membership. A directory, process, package, runtime or database belongs to a Park only when Identity recognizes the governing contract and placement.

An App or Engine contract must identify enough to materialize and recover the resident, including:

- stable identity and owner/principal;
- recognized source/artifact version;
- placement;
- lifecycle state;
- capabilities provided/consumed;
- state-store declarations and authority;
- health/verification interface;
- required service relationships;
- resource requirements where material;
- install, upgrade, retirement and recovery semantics;
- secret references, never secret values.

## Onboarding law

Onboarding is a Continuity workflow executed from an adopted contract, not “clone and start”.

Working V0 uses Google ADK Workflow Engine to orchestrate onboarding.

```text
recognized App / Engine Contract
        ↓
validate identity, authority and template
        ↓
Google ADK onboarding workflow
        ↓
select declared LAB / Park
        ↓
materialize software + runtime relationships
        ↓
provision declared state stores
        ↓
configure secret/provider bindings
        ↓
verify health and declared effects
        ↓
receipt + census evidence
        ↓
recognize resulting materialization
```

The durable law is:

> **Declare → Materialize → Prove → Recognize**

## CloudKit provisioning

Apple infrastructure is treated as a replaceable provisioning substrate. The existing CloudKit data/schema may be wiped and rebuilt.

Powerfarm MUST preserve or be able to recreate the Apple developer capability required for remote programmatic provisioning, including the developer account relationship, container identity, signing/provisioning material and required keys/certificates.

For **private CloudKit data**, the provisioning unit is a private-database custom record zone/namespace. Apple permits custom zones only in the owning user's private database, and server-to-server keys alone administer the public database. Therefore V0 private provisioning requires a **user-authenticated Apple provisioner** acting as the Director's iCloud owner identity on an always-on ecosystem LAB, or an equivalent user-authenticated CloudKit Web Services flow.

The control request may originate remotely, but the authenticated Apple execution path MUST NOT depend on LAB 256.

CloudKit's final V0 role is the database/namespace substrate for admitted App Park applications and Engine Park engines when their contracts require it.

Continuity provisions those databases during onboarding according to the contract.

The contract must declare, at minimum:

- store id;
- owner app/engine;
- purpose;
- authority scope;
- container/environment/database/zone locator;
- schema/migration identity;
- durability and backup rule;
- searchability;
- sensitivity;
- retirement/recovery semantics.

The database contents remain operational state owned by that app or engine. The Registry records the declaration and relationship, not the app's ordinary rows.

Current container:

`iCloud.app.powerfarm`

CloudKit identity does not replace Powerfarm identity.

### Legacy CloudKit deletion law

Historical Apple-first Registry/test records are negative delta with terminal disposition `DELETE`.

The Director has classified that state as disposable test material. Exact record-by-record enumeration is no longer a cleanup gate. The signed census and existing receipts preserve sufficient evidence; the historical data/schema may be wiped and rebuilt while preserving/recreating the provider capability above.

At convergence, CloudKit contains only contract-owned app/engine databases/namespaces. No company Registry authority remains there.

## Host Runner

Each ecosystem LAB has one deterministic Host Runner boundary for approved machine-changing work.

The Host Runner:

- executes allow-listed jobs;
- checks preconditions and protected paths;
- produces receipts;
- reports health;
- does not grant itself authority;
- does not treat LLM output as approval.

Google ADK may orchestrate a workflow; the Host Runner remains the controlled local effect boundary where the workflow requires machine changes.

## Agents

One agent per LAB (`pf.agent.lab-8gb`, `pf.agent.lab-512`; `pf.agent.lab-256` on the bench, never required):

- the only launchd service allowed besides protected processes and remote-access tunnels; installed by its installer, with health check and automatic rollback;
- releases go LAB 256 → LAB 512 → LAB 8GB; the two ecosystem LABs never update together;
- observes: signals every minute, inventory every 15 minutes, a copy of every conversation event, all written to the Antenna store;
- converses with the Director through Coloured Places over a tunnel, accepting only short signed tokens;
- proposes; it never executes machine changes itself: those go through the Host Runner after approval;
- holds the Engineer office; its autonomy per operation class follows V0-01 §2.8.

LAB 8GB is the principal: it also watches the cloud places (Identity substrate, apps, engines, archive). LAB 512 is the reserve and takes over when the principal is silent.

## Experiments and dependencies

- **Experiments run only through a ticket:**
  - the ticket records the owner, project, requesting session, purpose, port and expiry (default 3 days);
  - an expired experiment stops by itself;
  - promotion makes it permanent through a contract.
- **A service created outside the agent** (plist, cron, process manager, tunnel) is shown as "present and must not" and proposed for quarantine.
- **Dependencies:**
  - one package store per machine;
  - shared build caches;
  - clone-based deduplication of identical files;
  - rebuildable folders pruned from idle projects;
  - versions follow a policy (newest LTS for Node, newest stable otherwise), applied in code by a bot with tests.

## Admission and delta rule

A required resident is not complete until:

1. its Registry identity and recognized version exist;
2. its contract is adopted;
3. placement and required grants/secret references are declared;
4. Continuity materializes it;
5. required stores/relationships are provisioned;
6. verification passes;
7. census observes the expected resident.

An observed app/engine/process that is not explained by protected human/system rules, an adopted contract, or a declared temporary migration exception is negative-delta material.

Its disposition comes from the finite V0 delta model.

## Exit criteria

Continuity V0 is converged when every App Park and Engine Park resident is explained by an adopted contract, every adopted resident has verified materialization, and CloudKit contains only contract-owned app/engine databases.
