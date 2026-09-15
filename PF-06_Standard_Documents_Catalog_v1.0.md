**POWERFARM CANON**

Standard Documents Catalog

A registry of document types and dormant future documents that may be created only when reality asks for them

| **DOCUMENT**  | PF-06                    |
|---------------|--------------------------|
| **STATUS**    | **REGISTRY - NOT CANON** |
| **VERSION**   | 1.0                      |
| **EFFECTIVE** | 15 September 2026        |

| **OWNS**         | Which reusable document types Powerfarm recognizes, the minimum shape of each, and which future Powerfarm-specific documents are intentionally dormant until a trigger appears. |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **DOES NOT OWN** | Current institutional truth. Listing a document here does not create a rule, project, deadline, owner, or obligation to write it.                                               |

> **Default outcome**
>
> The default result of reviewing this catalog is to create nothing. A document is instantiated only when a concrete recurring need, risk, decision, or coordination problem makes it useful.

# 1. How to use this catalog

1.  Identify the real operational need or decision.

2.  Check whether PF-01 through PF-05 already contain the required durable truth.

3.  Check whether an existing standard instance can be updated instead of creating another document.

4.  If a new artifact is useful, choose the smallest standard type that fits.

5.  Create only the fields needed for the consequence of the work.

6.  Assign an owner and a review, supersession, or retirement condition when the document is expected to live.

7.  Archive or delete the artifact when it no longer has an active reader, decision, or historical purpose.

# 2. Document states

| **State**    | **Meaning**                                                                         |
|--------------|-------------------------------------------------------------------------------------|
| DRAFT        | Being written or tested. Not authoritative outside its explicit working scope.      |
| ACTIVE       | Current standard instance for its defined scope.                                    |
| UNDER REVIEW | Current state is being reassessed; use with caution.                                |
| SUPERSEDED   | Replaced by a newer artifact. Preserved for history.                                |
| ARCHIVED     | No longer active but retained for reference or institutional memory.                |
| RETIRED      | The document type or specific artifact no longer provides enough value to maintain. |

# 3. Universal minimum metadata

A durable standard instance SHOULD contain only the metadata that helps someone use or maintain it. For consequential documents, the default minimum is: title, purpose/scope, owner, state, version or date, current decision/rule/output, material evidence or dependencies, and review/supersession trigger.

Codes and numbering are optional. Powerfarm does not reserve dozens of empty numbered documents in advance.

# 4. Standard document types

## 4.1 Governance and decisions

| **Standard type**        | **Create when**                                                                        | **Minimum content**                                                                       |
|--------------------------|----------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|
| Decision Record          | A consequential choice may need to be understood or reversed later.                    | Decision, owner, context, options, evidence, consequences, trigger, date.                 |
| Policy / Standard        | A recurring rule must apply across multiple decisions or artifacts.                    | Purpose, scope, mandatory/default rules, exceptions, owner, change trigger.               |
| Exception Record         | A material departure from a rule is justified temporarily or conditionally.            | Rule, reason, evidence, consequence, owner, expiry/review trigger.                        |
| Role Charter             | A recurring role has ambiguous authority, interfaces, or outcomes.                     | Purpose, outcomes, authority, responsibilities, interfaces, review trigger.               |
| Resource Allocation Memo | A material allocation of money, compute, hardware, or human attention needs rationale. | Goal, options, constraints, allocation, expected value, opportunity cost, review trigger. |
| Risk Register            | Multiple active risks need ongoing ownership rather than one-off discussion.           | Risk, likelihood/impact if useful, owner, mitigation, signal, next review.                |
| Institutional Review     | Behavior may be drifting from canon or a durable rule may be wrong.                    | Observed gap, evidence, affected rule, options, decision, owner, follow-up.               |

## 4.2 Research and evidence

| **Standard type**                 | **Create when**                                                                       | **Minimum content**                                                                                                |
|-----------------------------------|---------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| Research Question Brief           | A frontier change, customer problem, or unresolved choice may justify research.       | Decision question, current belief, existing evidence, value of information, priority.                              |
| Study / Experiment Plan           | A comparison or confirmatory test needs pre-specified design.                         | Hypothesis, unit under test, comparators, tasks, outcomes, budget, exclusions, analysis, verification.             |
| Experiment / Run Record           | A significant execution should contribute to longitudinal evidence.                   | Environment, configuration, inputs, outputs, measurements, failures, cost, verification, timestamp.                |
| Benchmark / Test Bench Definition | A reusable measurement instrument is needed.                                          | Decision scope, tasks, unit under test, environment, resource regime, metrics, graders, versioning, comparability. |
| Evidence Summary                  | A claim or decision depends on several evidence paths.                                | Claim/question, supporting and contradicting evidence, limitations, freshness, confidence.                         |
| Claim and Confidence Record       | A living claim needs explicit scope and reassessment.                                 | Claim, scope, evidence links, confidence, exceptions, last review, retest trigger.                                 |
| Research Report                   | A completed body of work should be communicated or sold.                              | Question, method, results, uncertainty, limitations, conclusions, recommendations, evidence lineage.               |
| Replication Record                | A prior result is important enough to test again.                                     | Target result, replication differences, result, comparability, interpretation, confidence impact.                  |
| Technology Evaluation             | A new model/tool/provider/protocol may change current practice.                       | Affected decisions, candidate, incumbent, test plan, evidence, promote/pilot/reject status, retest trigger.        |
| Epistemic Incident Review         | A high-confidence material claim or recommendation was seriously wrong or misleading. | Incident, impact, root cause, affected claims, corrections, method changes, calibration action.                    |

## 4.3 Technology and software

| **Standard type**                   | **Create when**                                                                  | **Minimum content**                                                                                              |
|-------------------------------------|----------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|
| System / Architecture Specification | A technical system has enough moving parts that shared structure is necessary.   | Purpose, boundaries, interfaces, data/control flow, constraints, invariants, failure modes, replacement trigger. |
| Architecture Decision Record        | A technical choice has meaningful alternatives or migration cost.                | Context, decision, alternatives, evidence, consequences, reversal trigger.                                       |
| Build vs Use Evaluation             | Proprietary infrastructure is being considered.                                  | Need, external alternatives, differentiated value, cost, lock-in, replaceability, decision, review trigger.      |
| Runbook / Playbook                  | A recurring operation benefits from a repeatable sequence.                       | Trigger, inputs, ordered actions, outputs, completion criteria, exceptions, escalation.                          |
| Security Review                     | A change introduces material secrets, access, sensitive data, or attack surface. | Assets, trust boundaries, threats, controls, residual risk, owner, review trigger.                               |
| Technical Incident / Postmortem     | A failure can recur or exposed a systemic weakness.                              | Event, impact, timeline, causal factors, detection, recovery, actions, owners, follow-up.                        |
| Data Specification                  | A durable data object or interface requires shared semantics.                    | Entities/fields, meaning, provenance, retention if relevant, validation, versioning, consumers.                  |

## 4.4 Products and business

| **Standard type**                | **Create when**                                                                         | **Minimum content**                                                                                         |
|----------------------------------|-----------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| Product Brief                    | A possible product deserves structured consideration.                                   | Customer decision/problem, evidence of demand, value, differentiation, product class, risks, next test.     |
| Product Specification            | A product is actively being built or maintained.                                        | Users, outcomes, scope, requirements, evidence claims, quality bar, metrics, constraints, release criteria. |
| Customer Research Brief          | A customer segment or problem needs discovery before product decisions.                 | Question, target users, evidence plan, observations, patterns, implications, uncertainty.                   |
| Commercial Research Scope        | A bespoke paid research engagement is being defined.                                    | Decision question, scope, data boundaries, method, deliverables, confidentiality, acceptance, exclusions.   |
| Pricing Memo                     | Price or commercial packaging is consequential enough to need rationale.                | Customer value, alternatives, costs, packaging, assumptions, decision, experiment/review trigger.           |
| Launch / Publication Plan        | A release has enough coordination, claim, or customer risk to plan explicitly.          | Audience, release scope, evidence/claim review, distribution, support, rollback/correction plan.            |
| Vendor / Partnership Memo        | An external relationship creates material dependency, access, conflict, or opportunity. | Purpose, counterpart, value, dependencies, disclosure/conflict, data/security boundary, exit trigger.       |
| Correction / Supersession Notice | A published product or claim materially changes.                                        | Prior state, correction/change, reason, affected outputs, current state, date.                              |

# 5. Dormant Powerfarm future documents

The following are recognized candidates, not a roadmap. Each stays dormant until its trigger appears. Until then, the relevant canonical document is sufficient.

| **Dormant candidate**                     | **Trigger to create**                                                                                                                                         | **Until then**                 |
|-------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------|
| Research Portfolio and Question Selection | Research opportunities routinely exceed capacity and ad hoc prioritization starts causing repeated conflict or poor allocation.                               | PF-02 / PF-03                  |
| Evidence Architecture Specification       | The evidence corpus becomes large or interconnected enough that inconsistent schemas, provenance, or immutability rules materially impair research.           | PF-02 / PF-04                  |
| Intelligence Matrix Specification         | Route/model/provider evidence becomes an operational dataset used repeatedly for routing or product decisions.                                                | PF-04                          |
| Cognitive Planning and Routing Method     | Automated or repeated cognitive planning becomes important enough that routing logic needs shared, testable rules.                                            | PF-04                          |
| Software Fabric Specification             | Multiple systems or teams need a detailed shared model for context, representation, change, and verification beyond PF-04.                                    | PF-04                          |
| Evaluation System Specification           | Evaluator selection, grader validation, and independent verification become complex enough to require a dedicated system design.                              | PF-02 / PF-04                  |
| Benchmark Operations Manual               | Powerfarm operates enough recurring benchmarks that execution, contamination, invalidation, grader calibration, and retesting need a repeatable manual.       | PF-02                          |
| Belief and Decision Model Specification   | Claims, confidence, dependencies, and conditional recommendations become machine-operated at meaningful scale.                                                | PF-02 / PF-04                  |
| Technology Surveillance Playbook          | The flow of relevant frontier changes becomes too large for ad hoc review and missed changes begin creating frontier drift.                                   | PF-04                          |
| Experimental Infrastructure Architecture  | Laboratory infrastructure has enough durable components, failure modes, or operators that a current architecture document saves real coordination cost.       | PF-04                          |
| Compute Allocation Policy                 | Local/cloud/hosted compute allocation creates repeated material budget, privacy, or capacity conflicts.                                                       | PF-03 / PF-04                  |
| Security and Secrets Standard             | Powerfarm handles enough sensitive systems, credentials, customer data, production access, or compliance obligations that the PF-04 baseline is insufficient. | PF-04                          |
| Data Governance Standard                  | Retention, client data, licensing, anonymization, deletion, or dataset eligibility become recurring material decisions.                                       | PF-04 / PF-05                  |
| Research Commercialization Policy         | Research-to-product decisions become frequent enough that PF-05 productization rules need a detailed repeatable policy.                                       | PF-05                          |
| Individual Research Engagement Method     | Bespoke customer research becomes a repeated line of business with recurring methodological, confidentiality, and ownership questions.                        | PF-05 / PF-02                  |
| Internal Software Development Method      | Powerfarm software development reaches enough scale or repeated contributors that PF-03/PF-04 no longer provide sufficient operating consistency.             | PF-03 / PF-04                  |
| Cost and Resource Allocation Policy       | API, hardware, compute, and opportunity-cost decisions become frequent enough to justify quantitative allocation rules.                                       | PF-03                          |
| Failure, Incident and Learning Protocol   | Incident volume or consequence makes the PF-03 learning baseline insufficient for consistent review.                                                          | PF-03                          |
| Institutional Memory and Archival Policy  | Historical volume, legal retention, retrieval difficulty, or record inconsistency starts causing loss of institutional memory.                                | PF-03 / PF-04                  |
| Publication and Corrections Standard      | Publication volume and revision frequency create recurring ambiguity about versions, corrections, retractions, and citations.                                 | PF-02 / PF-05                  |
| Research Ethics and Disclosure Policy     | Human data, private repositories, customer evidence, sensitive findings, sponsorship, or responsible disclosure create recurring ethical decisions.           | PF-02 / PF-05                  |
| Terminology and Concept Model             | Terminology inconsistency begins causing real misunderstanding across research, products, software, or external publication.                                  | All canon; default owner PF-03 |

# 6. Promotion to canon

A standard instance or dormant candidate does not become canonical merely because it is important. Powerfarm SHOULD add a new canonical document only if all of the following are true:

- The subject defines durable company-wide truth rather than one system, workflow, product, or period.

- The truth cannot fit cleanly into PF-01 through PF-05 without distorting their purpose.

- The need has appeared repeatedly in real operations, not only in anticipation.

- The maintenance owner and audience are clear.

- The cost of another source of truth is lower than the ambiguity it removes.

> **Default canon decision**
>
> Amend one of the five before creating a sixth canonical document.

# 7. Retirement and consolidation

A standard instance SHOULD be retired, merged, or archived when it no longer changes a decision, when the need disappears, when another document becomes the one true home, or when maintaining it costs more than the confusion it prevents.

Retirement preserves historically important decisions and evidence but removes the artifact from active authority. Historical usefulness is not the same as current authority.

# 8. Naming rule

Names should describe the artifact a reader is looking for. Use plain titles first. Add a date, version, system, product, customer, or decision subject only when it disambiguates. Avoid pre-allocating identifier ranges or empty document slots.

> **Catalog principle**
>
> Recognize useful forms in advance. Instantiate them only when reality creates the need. The catalog is a toolbox, not a construction schedule.
