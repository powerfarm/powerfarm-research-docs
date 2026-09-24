# V0-05 - Ideal Registry V0

**Status:** WORKING V0 target I, recognized at `6438c55a20e82e922322d26561487f91761a6e3a`  
**Purpose:** define the finite institutional state Powerfarm intends to recognize for V0.

Ideal Registry V0 is not a list of every byte, process, package or historical project. It is the finite set of identities, versions, contracts, grants, stores, placements and required relationships that make V0 coherent.

The machine-readable companion is `registry-v0.yaml`.

## Admission law

An item belongs in Ideal Registry V0 only when it has a V0 institutional purpose.

Every required item must resolve to one or more of:

- entity;
- artifact;
- artifact version;
- contract;
- grant;
- declared store;
- placement/topology relationship;
- capability;
- Search surface/source;
- documented temporary exception.

Anything else may still exist in the world, but it is not part of Ideal Registry V0.

## V0 institution

### Human

- Director principal.

### Machines

- `pf.lab-8gb`
- `pf.lab-512`
- `pf.lab-256`

### Durable architectural systems

- `pf.identity`
- `pf.continuity`
- `pf.antenna`
- `pf.heartime`
- `pf.research`
- `pf.minivault`
- `pf.search`

These are semantic responsibilities. Their implementation may consist of several artifacts/services.

### Infrastructure/control-plane entities

- Powerfarm Supabase company plane, bound for working V0 to Supabase project ref `ekjlmclhqnsstfjzuabz` (provider-side name `powerfarm.kernal`, region `eu-west-1`). The provider project name is not the institutional identity; `pf.store.supabase.company` is.
- CloudKit container `iCloud.app.powerfarm` as adopted Apple project-vault substrate.
- one Host Runner installation per LAB.
- Powerfarm Search Supabase source.
- Powerfarm Search CloudKit source.
- Airtable Search projection.
- adopted content/byte storage and backup replicas.
- GitHub source-control repositories that V0 explicitly recognizes.

### Research canon artifacts

V0 recognizes exact versions of:

- PF-01
- PF-02
- PF-03
- PF-04
- PF-05
- PF-06

The merge commit that adopts this V0 package becomes the initial recognized version reference for this architecture package.

### Core V0 specifications

The following are recognized architecture-spec artifacts once merged:

- V0-01 Minivault, Storage and Registry
- V0-02 App Park, Engine Park and App Contracts
- V0-03 Namespace, Authority and Secrets
- V0-04 Current Registry Situation
- V0-05 Ideal Registry V0
- PF-03/PF-04 deconstruction map
- `registry-v0.yaml`

## V0 stores

Required logical stores are:

1. company Registry store;
2. company operational/job/receipt store;
3. company adopted Minivault store where required;
4. CloudKit project-vault store(s);
5. immutable byte/content store(s);
6. rebuildable Search/index/projector stores;
7. local transactional/runtime stores only where an application contract requires them.

A store is admitted through an App Contract/Store declaration, not by filesystem discovery.

## V0 contracts

At minimum V0 must recognize:

- App Contract for each admitted application;
- Host Runner machine/application contract per LAB;
- Search Contract for every searchable source;
- store authority declarations;
- machine/place relationships;
- secret-consumer relationships;
- execution/approval contract for destructive/system-changing jobs;
- backup/custody contract for material company bytes;
- research canon artifact/version relationships.

A subordinate contract may remain embedded in a root App Contract when splitting it would add ceremony without reducing ambiguity.

## V0 authority

V0 must be able to answer mechanically:

- who/what may read a protected store;
- who/what may write or publish;
- who may approve a destructive/system effect;
- which application owns each mutable store;
- which store is authoritative for each class of state;
- which projections are non-authoritative.

No grant may be inferred from network access, account possession, path ownership or Park placement.

## V0 Search

Powerfarm Search must federate recognized company and project sources.

Required initial sources:

- Supabase company source;
- CloudKit project source.

Required initial human projection:

- Airtable.

Search does not own canonical state.

## V0 Parks

Each LAB must converge to:

- protected human/system material;
- one Powerfarm institutional root;
- App Park containing only contract-admitted apps;
- Engine Park containing only contract-admitted shared engines;
- minimum required local dot-state/tool configuration;
- one Host Runner.

Historical projects may be preserved outside the admitted Parks or archived. Presence outside a Park is not necessarily negative delta; disposition depends on ownership/history/protection.

For Git repositories, working V0 designates GitHub organization **`powercitty`** as the historical-preservation organization for superseded Powerfarm repositories. Transfer to Powercitty is an archival disposition, not destruction, and does not by itself confer active V0 Registry membership.

## V0 secret policy

The Registry contains secret references and metadata only.

No live credential value belongs in:

- this public repository;
- Airtable;
- Search indexes;
- receipts;
- ordinary CAS/content archives.

## V0 completion condition

V0 is converged when:

```text
C - I = empty except explicit non-destructive dispositions/deferred exceptions
I - C = empty
post-convergence census matches adopted topology
Current Registry digest = adopted Ideal Registry V0 digest
```

In practical terms:

- every negative-delta observation has a disposition and completed receipt or explicit retained exception;
- every positive-delta item has been built/materialized/registered and verified;
- every admitted app/store has a contract and owner;
- every material company byte has verified custody;
- Search can explain its sources;
- Airtable is rebuildable from Search;
- both the architecture and materialization are recoverable from recognized source and evidence.
