**POWERFARM CANON**

Specifications and Records Catalog

How Powerfarm keeps exactly two layers of document authority: six canonical documents and the Specifications that implement them

| **DOCUMENT**  | PF-06 |
|---|---|
| **STATUS**    | **CANONICAL** |
| **VERSION**   | 2.0 |
| **EFFECTIVE** | 27 September 2026 |

| **OWNS** | The document authority model; Specification creation, scope, lifecycle, naming, supersession, and minimum metadata; and the recognized forms of non-authoritative supporting records. |
|---|---|
| **DOES NOT OWN** | The substantive institutional truth owned by PF-01 through PF-05, or the system-specific behavior owned by an adopted Specification. |

> **Document constitution**
>
> Powerfarm has six canonical documents and one subordinate authoritative document form: the Specification. Everything else is supporting evidence, working material, or history.

# 1. Authority model

Powerfarm deliberately keeps document authority small.

```text
CANON
PF-01 ... PF-06
        ↓ governs
SPECIFICATIONS
        ↓ implemented by
code / services / workflows / products
```

The six canonical documents are:

1. PF-01 Powerfarm Charter.
2. PF-02 Research and Evidence Standard.
3. PF-03 Powerfarm Operating System.
4. PF-04 Intelligence and Technology System.
5. PF-05 Products and Business System.
6. PF-06 Specifications and Records Catalog.

A Specification is authoritative within its stated scope and MUST conform to all applicable Canon rules. A Specification MAY refine, operationalize, or choose among implementation alternatives left open by Canon. It MUST NOT silently redefine a Canon invariant.

There is no third authoritative document class.

Notes, proposals, decision records, research plans, run records, evidence summaries, reports, incident records, external references, and superseded material MAY exist when useful. Their existence does not make them authoritative. Authority arises only from Canon or an adopted Specification.

# 2. Canon and Specification change

## 2.1 Canon

Canon changes only when Powerfarm deliberately changes durable institutional truth. A Canon change MUST preserve the superseded version and state why the new rule is better.

The active Canon is exactly PF-01 through PF-06. Creating a seventh canonical document requires an explicit amendment to PF-01 and this document. The default is to amend one of the six.

## 2.2 Specifications

A Specification exists because a bounded behavior needs one authoritative technical home. Typical subjects include:

- Registry and recognition semantics;
- contracts and contract lifecycles;
- onboarding and admission;
- schemas and data models;
- protocols and interfaces;
- names and addressing;
- identity and authentication;
- content storage and immutable representation;
- execution and Continuity;
- Antenna, Heartime, Search, and projections;
- language profiles;
- security or data-handling mechanisms;
- maintained product behavior.

A Specification SHOULD be created only when the behavior is sufficiently durable, shared, or consequential that leaving it implicit would create repeated ambiguity, incompatible implementations, hidden authority, or operational risk.

# 3. Specification lifecycle

| **State** | **Meaning** |
|---|---|
| DRAFT | Being designed or tested. Not institutionally authoritative. |
| ACTIVE | Adopted and authoritative within its stated scope. |
| UNDER REVIEW | Still current, but material revision or replacement is being evaluated. |
| SUPERSEDED | Replaced by a newer Specification. Preserved for history and rebuildability. |
| RETIRED | No longer defines active behavior. Preserved when historically material. |

A DRAFT may be implemented experimentally. Experimental implementation does not make the draft authoritative. Adoption is explicit.

# 4. Minimum Specification shape

A Specification SHOULD remain as small as its responsibility allows. A consequential Specification normally identifies:

```text
title
status
version / effective date
purpose
scope
canonical basis
owned responsibility
explicit non-responsibilities
terms / types
invariants
contracts / schemas / interfaces
state or lifecycle where relevant
authority and security boundaries
failure / uncertainty semantics
verification / conformance
migration / supersession rules where relevant
dependencies
```

Not every Specification needs every field. Structure follows consequence.

# 5. Specification families

The following are reusable shapes, not separate authority classes.

| **Specification shape** | **Use when** |
|---|---|
| Contract Specification | A relationship, authority model, lifecycle, or admission rule needs machine-readable common semantics. |
| System / Architecture Specification | A technical system has enough durable shared structure to require one implementation contract. |
| Data / Schema Specification | Data meaning, validation, provenance, versioning, or compatibility must be shared. |
| Interface / Protocol Specification | Independent components need a stable interaction boundary. |
| Language Profile | A production language needs one adopted toolchain and engineering baseline. |
| Operational Specification | A recurring consequential operation requires deterministic inputs, actions, outputs, verification, and exception behavior. |
| Security / Data Specification | Repeated security, privacy, secret, retention, or trust-boundary behavior needs one durable implementation rule. |
| Product Specification | A maintained product needs authoritative behavioral, quality, interface, or release requirements. |

A single Specification MAY combine shapes when one coherent responsibility would otherwise be fragmented.

# 6. Contract-first rule

Institutional relationships and authority are represented through contracts. Specifications define contract schemas and interpretation; they do not create parallel grant systems.

Where a recurring relationship becomes operationally important, Powerfarm SHOULD first ask whether it is a contract type before inventing another authority primitive or document mechanism.

Examples include:

- grants and permissions;
- offices and office holding;
- role assignments and delegations;
- app admission;
- service relationships;
- store authority;
- memberships and placements;
- execution authority.

The App Contract is a first-class contract type because application onboarding, ownership, source, version, state authority, placement, capabilities, dependencies, lifecycle, and admission evidence need a common root relationship. Detailed subordinate relationships MAY live in their own contract types and Specifications.

# 7. Supporting records

Supporting records exist to preserve evidence and reasoning. They are not another authority layer.

Common useful forms include:

## 7.1 Governance and decisions

- Decision Record
- Exception Record
- Resource Allocation Record
- Risk Register
- Institutional Review

## 7.2 Research and evidence

- Research Question Brief
- Study / Experiment Plan
- Experiment / Run Record
- Benchmark / Test Bench Definition
- Evidence Summary
- Claim and Confidence Record
- Research Report
- Replication Record
- Technology Evaluation
- Epistemic Incident Review

## 7.3 Technical and operational evidence

- Architecture Decision Record
- Build-vs-Use Evaluation
- Technical Incident / Postmortem
- Security Review
- Verification Record
- Migration Record

## 7.4 Product and business evidence

- Product Brief
- Customer Research Brief
- Commercial Research Scope
- Pricing Record
- Launch / Publication Plan
- Vendor / Partnership Record
- Correction / Supersession Notice

These records MAY be referenced by Canon or Specifications as evidence. A record becomes authoritative only to the extent an authoritative document explicitly incorporates a rule or decision from it.

# 8. Candidate Specifications

Powerfarm MAY maintain names of plausible future Specifications so recurring gaps are visible. A candidate is not a roadmap, reservation, obligation, or empty numbered slot.

Examples of plausible future needs include:

| **Candidate capability** | **Create when** |
|---|---|
| Research Evidence Architecture | Evidence schemas, provenance, claims, confidence, and contradiction handling need shared machine behavior beyond PF-02. |
| Contracts and Onboarding | Contract lifecycle, authority derivation, App Contract, admission, and onboarding need one machine-authoritative model. |
| Continuity and Executability | Triggering, claims, effects, verification, retries, and recovery need one executable contract. |
| Antenna | Observational evidence ingress and semantics need a stable service contract. |
| Heartime | Temporal evidence and contractual temporal predicates need a stable service contract. |
| Federated Search | Cross-store discovery and projection behavior need one read-model contract. |
| Rebuild | Genesis, replay, verification, provider bootstrap, and recurring rebuild proof need one operational contract. |
| Intelligence Routing | Route, model, provider, cost, verifier, and escalation behavior become operationally reused. |
| Security and Secrets | The PF-04 baseline is insufficient for recurring sensitive-system decisions. |
| Data Governance | Retention, customer data, licensing, anonymization, or deletion become recurring implementation rules. |
| Product Interface | A maintained external product needs stable machine or service behavior. |

Candidate names SHOULD remain unnumbered until the Specification is actually instantiated.

# 9. Naming and numbering

Names should describe the artifact a reader is looking for.

Specification identifiers MAY be assigned when a Specification is instantiated. Powerfarm MUST NOT reserve empty numeric ranges or create phantom Specifications merely to preserve sequence.

A Specification name SHOULD remain meaningful even without its identifier.

# 10. Supersession and history

An ACTIVE Specification may be replaced only by explicit supersession. The replacement states what changed, compatibility or migration consequences where material, and which prior Specification it supersedes.

Historical material remains available when required to reconstruct institutional decisions, recognized state, or behavior. Historical usefulness does not create current authority.

# 11. Conformance rule

When Canon and a Specification appear to disagree:

1. determine whether the Specification merely refines implementation detail left open by Canon;
2. if it changes a durable invariant, treat the issue as a Canon conflict;
3. amend the Specification or explicitly amend Canon;
4. never resolve the conflict silently through implementation inertia.

When two active Specifications overlap, one responsibility MUST be made authoritative and the other must reference it. Competing definitions of the same concept are not allowed to persist as normal state.

# 12. Final rules

1. Powerfarm has exactly six active canonical documents.
2. Specifications are the only subordinate authoritative document form.
3. Specifications MUST conform to Canon.
4. Drafts and supporting records are not authoritative merely because they exist.
5. Every durable technical or operational concept SHOULD have one authoritative home.
6. Grants, permissions, roles, admissions, and similar institutional relationships SHOULD be modeled as contract types rather than parallel authority primitives.
7. App Contract is a first-class contract type and the root contract for application onboarding.
8. Specification numbers are assigned only when Specifications actually exist.
9. Supersession preserves history.
10. When reality changes, amend the smallest authoritative document that actually owns the changed truth.

> **Catalog principle**
>
> Six documents define the institution. Specifications define its machinery. Everything else helps Powerfarm think, prove, and remember.
