**POWERFARM CANON**

Powerfarm Operating System

How Powerfarm decides, allocates work, changes, and keeps the company coherent without excess process

| **DOCUMENT**  | PF-03             |
|---------------|-------------------|
| **STATUS**    | **CANONICAL**     |
| **VERSION**   | 1.0               |
| **EFFECTIVE** | 15 September 2026 |

| **OWNS**         | Decision ownership, work lifecycle, build-vs-use, resource allocation, exceptions, institutional drift, documentation governance, and durable operating rules. |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **DOES NOT OWN** | Research methodology (PF-02), technical system design (PF-04), or product/commercial doctrine (PF-05).                                                         |

> **Normative language**
>
> MUST means required unless this canon is changed. SHOULD means the default and a material deviation needs a reason. MAY means optional.

# 1. Operating doctrine

Powerfarm is a small research institution operating in a fast-changing technical environment. Its operating system therefore optimizes for clarity, speed of learning, reversible change, and accumulated knowledge rather than procedural volume.

> **Minimum-process rule**
>
> A process, meeting, approval, template, or recurring artifact must earn its existence by reducing meaningful risk, coordination cost, repeated confusion, or loss of knowledge. If the cost of the process exceeds the expected cost of the failure it prevents, simplify or remove it.

# 2. Operating principles

| **Principle**                               | **Operating meaning**                                                                                                              |
|---------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| One owner                                   | Every consequential piece of work has one clearly accountable owner, even when many people or agents contribute.                   |
| Decision at the lowest competent level      | Escalate when authority, irreversible consequence, material risk, or cross-system conflict requires it, not by habit.              |
| Reversibility matters                       | Reversible decisions move quickly. Irreversible or expensive-to-reverse decisions receive proportionally more evidence and review. |
| Write the decision, not the theater         | A short durable record is preferred to a meeting whose reasoning disappears.                                                       |
| Default to action with explicit uncertainty | Uncertainty can coexist with action when the downside is bounded and the state is recorded.                                        |
| Build thin                                  | Custom infrastructure exists only where it creates differentiated Powerfarm value.                                                 |
| Preserve history                            | Current truth can change; prior truth remains reconstructable.                                                                     |
| Exceptions are data                         | Repeated exceptions indicate either operational drift or a rule that should change.                                                |
| Cadence follows need                        | Recurring rituals are created only when the underlying need recurs.                                                                |
| Automation serves judgment                  | Agents and automation reduce coordination and execution burden, but must not conceal ownership or evidence.                        |

# 3. Work lifecycle

1.  Sense: notice a change, problem, opportunity, request, failure, or unresolved decision.

2.  Frame: define the outcome, owner, constraints, and what evidence is already known.

3.  Decide: choose the next action at the appropriate level of rigor.

4.  Execute: perform the work with the smallest sufficient process and tools.

5.  Verify: check that the intended outcome occurred and that material risks are bounded.

6.  Learn: capture what changed our understanding, including failures and surprises.

7.  Update: revise the relevant current state, recommendation, product, system, or canon when justified.

Not every task needs a formal artifact for every stage. The lifecycle describes the logic that must remain available, not a mandatory seven-form workflow.

# 4. Decision ownership and records

A consequential decision SHOULD have one Decision Owner. Contributors may research, challenge, execute, or verify, but accountability remains explicit.

A durable Decision Record is required when a choice is expensive to reverse, changes a canonical rule, creates material proprietary infrastructure, materially affects customers or public claims, creates a security/privacy boundary, or is likely to be revisited later without obvious context.

| **Minimum field**  | **Question**                                          |
|--------------------|-------------------------------------------------------|
| Decision           | What are we choosing?                                 |
| Owner              | Who is accountable for the decision?                  |
| Context            | What problem or opportunity caused the decision?      |
| Options            | What credible alternatives were considered?           |
| Evidence           | What supports the choice, and what remains uncertain? |
| Consequences       | What do we gain, give up, or risk?                    |
| Reversal / trigger | What event should cause reconsideration?              |
| Date / version     | When did this become current?                         |

# 5. Decision classes

Powerfarm does not require a different bureaucracy for every kind of decision, but the evidence that matters differs by class.

| **Class**     | **Primary question**                                                                                                  |
|---------------|-----------------------------------------------------------------------------------------------------------------------|
| Research      | What decision could new evidence change, and how much rigor is justified?                                             |
| Technical     | Does this improve outcomes, evidence, reliability, safety, economics, or replaceability enough to justify complexity? |
| Product       | Does this convert Powerfarm knowledge into repeated external value without distorting research integrity?             |
| Resource      | What is the highest-value use of money, compute, hardware, and human attention under current constraints?             |
| Institutional | Does this alter a durable rule about what Powerfarm is or how it must operate?                                        |

# 6. Build versus use

> **Default**
>
> Use sufficiently capable external technology before building an equivalent proprietary component.

Before a material internal build, the owner SHOULD answer:

- Which Powerfarm outcome or canonical promise requires this capability?

- Which credible external alternatives were evaluated?

- What differentiated value would custom work create in evidence, knowledge, safety, reliability, economics, or decision capability?

- What maintenance and lock-in will Powerfarm inherit?

- How replaceable will the component remain?

- What measurable event would cause us to stop, replace, or simplify it?

If an external capability is sufficiently good and a proprietary implementation does not create material Powerfarm-specific value, Powerfarm SHOULD NOT build it.

# 7. Resource allocation

Powerfarm allocates scarce resources to maximize decision value and compounding knowledge, not activity. Resource decisions SHOULD consider:

- Decision consequence and expected value of better information.

- Strategic compounding: whether the work creates reusable evidence, methods, or product capability.

- Time sensitivity and frontier freshness.

- Reversibility and downside if wrong.

- Monetary cost, compute, hardware occupancy, and human attention.

- External leverage: whether buying, renting, or integrating is superior to building.

- Opportunity cost: what important work is displaced.

Budget is a constraint on the decision, not a prestige signal. Powerfarm may exchange time for money, money for higher quality, or redundancy for confidence when the decision warrants it.

# 8. Exceptions

Rules exist to improve decisions, not to punish reality. A material exception MAY be accepted when it is explicit and bounded.

| **Exception field** | **Requirement**                                        |
|---------------------|--------------------------------------------------------|
| Rule                | Which rule or default is being departed from?          |
| Reason              | Why is the exception better under current constraints? |
| Evidence            | What supports the exception?                           |
| Owner               | Who owns the consequence?                              |
| Expiry / trigger    | When must it be reconsidered?                          |
| Remediation         | What must change if the exception is temporary?        |

Recurring exceptions to the same rule are evidence. They SHOULD trigger either correction of behavior or revision of the rule.

# 9. Conformance without bureaucracy

Formal conformance review is reserved for decisions where contradiction would be materially costly: canonical changes, strong public claims, important customer commitments, significant proprietary builds, or security/privacy boundaries.

A review asks:

8.  Does the decision conflict with the Charter or another canonical rule?

9.  Is the relevant evidence strong enough for the consequence?

10. Were credible external alternatives considered?

11. Are uncertainty, trade-offs, and exceptions explicit?

12. Does the decision preserve replaceability and historical traceability where material?

13. Does the subject create real outcome, knowledge, safety, or economic value proportional to its complexity?

14. What future event should trigger reassessment?

The output is simple: CONFORMING, JUSTIFIED EXCEPTION, CHANGE REQUIRED, or CANON REVIEW. Powerfarm does not maintain conformance scoring for its own sake.

# 10. Institutional and frontier drift

Institutional drift is the gap between Powerfarm's actual behavior and its durable commitments. Frontier drift is the gap between current practice and the sufficiently mature technology frontier.

- Growing proprietary maintenance without corresponding knowledge or product value.

- Repeated reliance on stale evidence or recommendations.

- Vendor dependence that weakens independent judgment or replaceability.

- Benchmarks defended as products rather than replaced as instruments.

- Increasing human rescue while autonomy claims remain unchanged.

- Recurring exceptions that have become the real operating rule.

- A major external advance that makes the current technical approach materially inferior.

A drift review ends in one of four outcomes: correct behavior, accept a temporary deviation, change method/implementation, or revise canon.

# 11. Incidents and learning

A material technical, operational, customer, security, or epistemic failure SHOULD produce a learning record when the lesson is likely to recur. The purpose is not blame; it is to prevent repeated ignorance.

The record SHOULD capture event, impact, causal factors, detection, recovery, what signals were missed, actions, owner, and follow-up trigger. High-confidence research claims found seriously misleading are treated as epistemic incidents under PF-02.

# 12. Documentation system

Powerfarm deliberately separates authority from volume. Documents are classified by role:

| **Class**         | **Meaning**                                                                                                                                    |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| Canonical         | One of PF-01 through PF-05. Defines current institutional truth.                                                                               |
| Standard instance | A recurring document type from PF-06 instantiated because a real need exists. It can be authoritative within its scope without becoming canon. |
| Working           | Proposal, draft, investigation, notes, or active design. May change freely.                                                                    |
| Reference         | Useful explanation, evidence, report, external source, or technical detail that does not define company-wide truth.                            |
| Historical        | Superseded material retained to reconstruct decisions, methods, and past state.                                                                |

- One important concept has one canonical home.

- A new document is not created merely to avoid editing an existing one.

- PF-06 records possible future document types and candidates. Listing a document there creates no obligation to write it.

- The default response to a new documentation need is: can the existing canon or an existing standard instance absorb this cleanly?

- A document without an owner, reader, decision, or maintenance reason SHOULD be archived or deleted rather than kept "just in case."

# 13. Change and history

Powerfarm expects methods, products, systems, and recommendations to change. Material current-state changes are versioned. Supersession preserves the prior version, the reason for change, and the date the new state became current.

> **Anti-dogma rule**
>
> A research institution that never changes is failing. A research institution that changes without knowing why is also failing.

# 14. Meetings and recurring cadence

No meeting, report, review, or recurring ritual is canonical by default. A cadence is introduced only when a recurring coordination or risk problem exists, and it is removed when that need disappears. Asynchronous written state is preferred when it provides equivalent clarity with lower cost.

# 15. Operating rules

15. Keep authority small and explicit.

16. Let reversible decisions move quickly.

17. Write consequential decisions so future Powerfarm can understand present Powerfarm.

18. Use external capability before reproducing it internally.

19. Treat exceptions and incidents as evidence.

20. Let process scale with consequence, not with organizational anxiety.

21. Change implementation aggressively when reality improves.

22. Change canon deliberately when identity or durable operating truth changes.
