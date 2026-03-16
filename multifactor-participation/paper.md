# Multifactor Participation: A Protocol for Verifying Human Judgment in Consequential AI Operations

## Abstract

Human-in-the-loop governance is the standard response to AI risk in consequential domains. In practice, it often produces inertia: the human is present but not participating, approving outputs they did not shape. This paper argues that the deepest governance failures are not accuracy failures but category errors — cases where computation is treated as a legitimate substitute for judgment in tasks that require interpretation, liability, or participatory legitimacy by nature. It introduces Multifactor Participation (MFP), a governance protocol modeled on multifactor authentication. Where MFA verifies identity through categorically distinct factors, MFP verifies human judgment through three non-substitutable factors: computational, participatory, and accountability. Operations are classified by which factors they require, and execution is blocked unless the required factors are satisfied, producing HITL-only surfaces where no fully automated path exists by design. MFP is enforced through three verification controls: a Finesse-validator that detects spirit-letter divergence, a Methexis filter that verifies participatory formation, and a Leap-gate that requires explicit liability acceptance. Together these controls produce auditable artifacts proving not that an output was reviewed, but that the judgment path was authored by a human. A worked example in benefits adjudication illustrates the protocol end to end. MFP does not require visibility into model internals or resolve questions about machine consciousness. It asks only whether the task requires judgment and, if so, whether a human was verifiably present in its formation.

---

## 1. Introduction

Some tasks require accountable human judgment by nature, not merely because current models are imperfect. A benefits caseworker interpreting a hardship provision. A clinician accepting responsibility for a treatment decision under irreducible uncertainty. A hiring panel weighing competing claims of fitness that no scoring function can reconcile. These are not tasks that machines do poorly. They are tasks whose legitimacy depends on a human being present — not at the end, to approve, but throughout, to judge.

The standard response to AI risk in these domains is human-in-the-loop governance. In principle, HITL ensures that a human remains the decision-maker and the machine remains a tool. In practice, HITL often delivers the opposite. The machine produces the output. The human reviews it under time pressure, with limited visibility into how it was formed, and approves it. The approval is recorded. The governance requirement is satisfied. No one participated in anything.

This paper calls that pattern *inertia*: the state in which a human is technically present in an approval workflow but exercises no genuine judgment. Inertia is not a failure of training or interface design. It is a structural property of systems that treat human oversight as a gate at the end of an automated pipeline rather than as a constitutive element of judgment itself.

The deeper problem is that current governance frameworks do not distinguish between the human's presence and the human's participation. They verify that a human reviewed the output. They do not verify that the human shaped it. They ask whether the machine performed well. They do not ask whether the task was the kind of thing a machine should have been performing in the first place.

### The category error

This paper argues that the most consequential AI governance failures are category errors. A *category error*, as used here, is a structural misassignment: treating an operation that requires human judgment as though it required only computation. The error is not that the system performed badly. It is that the system was asked to perform a kind of work — interpretation, liability acceptance, participatory formation — that is not computational in nature, regardless of how capable the system is.

Consider a system that correctly applies the letter of a benefits eligibility rule to deny an application. The output is accurate. The rule was followed. But the denial defeats the rule's purpose because the applicant's situation falls into the gap between the rule's language and its intent. The system followed the rule. It did not — and cannot — judge whether following it was the right thing to do.

This is not a performance failure. A better model would follow the rule more precisely, not question whether following it serves the rule's purpose. The failure is categorical: the task required judgment about intent, and the system provided computation about syntax.

We call the boundary where this substitution becomes illegitimate the *event horizon*. As used in this paper, the event horizon is a governance classification concept, not a formally measurable threshold. It marks the point at which an operation should be treated as requiring human judgment for governance purposes — because the domain requires interpretation of purpose, acceptance of liability, or participatory formation of the judgment. In practice, the event horizon is identified during operation classification (Sections 5.4-5.5), not detected automatically. Beyond it, the system may continue to produce fluent, useful, statistically strong outputs. But those outputs cannot carry the governance weight that the domain requires.

This paper adopts the position that some operations should be treated as judgment-requiring by nature, not merely because current models are limited. Even if models improve substantially, capability does not dissolve the governance need for accountable human ownership in domains involving interpretation of institutional purpose, liability acceptance, or participatory legitimacy. A more capable model follows a rule more precisely; it does not question whether following the rule serves the rule's purpose, accept personal liability for the outcome, or participate in the judgment as a responsible subject. These are not capability gaps. They are category boundaries.

### What this paper proposes

This paper introduces Multifactor Participation (MFP), a governance protocol for verifying that human judgment is present in consequential AI operations. MFP is a protocol, not a metaphor. It is modeled on multifactor authentication (MFA), which established that sensitive operations require categorically distinct verification factors for identity. MFP applies the same architecture to judgment.

MFP defines three factors:

- A **computational factor**: the system performed its function — retrieval, analysis, recommendation, consistency check.
- A **participatory factor**: a human shaped the reasoning path — set or reviewed constraints, observed decision-relevant checkpoints, exercised redirect capability at decision forks.
- An **accountability factor**: a named human accepted liability for the outcome — explicitly acknowledged the irreducible uncertainty and signed the decision as theirs.

The factors are categorically distinct. Satisfying one does not satisfy another.

Operations are classified by which factors they require. Some operations — document extraction, summarization, routing — require only the computational factor and can be fully automated. Others — eligibility determinations, treatment decisions, hiring decisions — require all three factors, and execution is blocked unless the required factors are satisfied. For these operations, no fully automated path exists by design. The architectural implications of this constraint are developed in Section 8.

MFP is enforced through three verification controls:

- The **Finesse-validator** detects when the system has satisfied the letter of a rule while violating its spirit.
- The **Methexis filter** verifies that the human participated in the formation of the output, not merely approved it after the fact.
- The **Leap-gate** requires a named human to accept liability for the outcome before execution proceeds.

Each control produces an auditable artifact. The artifacts do not prove that the output was correct. They prove that the judgment path was authored by a human.

This paper makes three contributions. First, it identifies a governance failure mode — human presence without participatory authorship — which it calls *inertia*. Second, it proposes Multifactor Participation (MFP), a protocol for classifying operations by required governance factors and verifying those factors at execution time. Third, it specifies verification controls and audit artifacts that produce structured evidence of whether a human participated in forming a judgment, not merely approving its result.

The paper does not argue that AI is useless in governance, demand open weights, or attempt to resolve questions about machine consciousness. It asks only whether the task requires judgment, and if so, whether a human was verifiably present in its formation.

The rest of the paper proceeds as follows. Section 2 situates MFP against related work. Section 3 describes three failure modes. Section 4 introduces methexis as participatory formation. Section 5 presents the protocol. Section 6 describes the verification controls. Section 7 walks through a worked example. Sections 8-10 address system design, limitations, and conclusion.

---

## 2. Related Work

The problems MFP addresses are not new. Several research traditions have identified the failure modes that arise when human oversight of automated systems is structurally inadequate. MFP's contribution is not the diagnosis — it is the protocol.

This asymmetry is deliberate. The oversight, accountability, and decision-support literatures are indispensable for diagnosing adjacent failures and clarifying institutional constraints, but they do not supply the paper's core concept of participation. MFP's conceptual foundation is drawn instead from a tradition in which participation is constitutive rather than merely procedural or informational. That is why the paper engages mainstream governance literatures as diagnosis and stress-test, while drawing its central account of participatory formation from a different source.

### Automation bias and complacency

A substantial empirical literature documents automation bias: the tendency of human operators to defer to automated recommendations even when those recommendations are incorrect (Parasuraman & Manzey, 2010; Mosier & Skitka, 1996). Automation complacency — reduced vigilance when a system appears reliable — compounds this effect over time. These findings describe at the empirical level exactly what this paper calls *inertia*: the human is present but not exercising genuine judgment. MFP extends this diagnosis from an observed behavioral tendency to a structural governance problem, and proposes a protocol for detecting and preventing it.

### Meaningful human control

The concept of meaningful human control (MHC) emerged from the autonomous weapons domain (Santoni de Sio & van den Hoven, 2018) and has been applied more broadly to AI governance. MHC requires that humans have sufficient understanding and control over a system's operation to be held responsible for its outcomes. MFP shares MHC's commitment to genuine human involvement rather than nominal oversight, but operationalizes it differently: where MHC frameworks specify conditions for control, MFP specifies a verification protocol that produces auditable evidence of participatory formation.

### Human oversight in regulatory frameworks

The EU AI Act requires human oversight for high-risk AI systems, including the ability to understand the system's capabilities and limitations, to monitor its operation, and to intervene or override its outputs. The NIST AI Risk Management Framework (AI RMF) similarly emphasizes human oversight as a governance mechanism. Both frameworks establish that human involvement is necessary. Neither specifies how to verify that the involvement was meaningful — whether the human shaped the judgment or merely received and approved a finished output. MFP addresses this gap.

### Algorithmic accountability and auditability

Work on algorithmic accountability (Raji et al., 2020; Selbst et al., 2019) has established the importance of audit trails, impact assessments, and institutional accountability mechanisms for AI systems. MFP builds on this tradition by specifying what the audit trail should contain: not just a record that a human was involved, but structured evidence of constraint-setting, checkpoint observation, redirect capability, and explicit liability acceptance.

### Levels of automation

The levels-of-automation taxonomy (Sheridan & Verplank, 1978; Parasuraman, Sheridan & Wickens, 2000) provides a graduated scale from full human control to full automation, with intermediate levels involving shared authority. MFP's operation classification (Class 1/2/3) echoes this taxonomy but applies it specifically to governance verification rather than to the degree of system autonomy. The key difference is that MFP's classification determines not how much the system does, but which verification factors must be satisfied before the system's output can be executed.

### Contestability

Recent work on contestability in AI systems (Almada, 2019; Henin & Le Métayer, 2021) argues that affected individuals should have the ability to challenge automated decisions. MFP's redirect capability — the requirement that humans can alter the system's path at decision forks — is closely related. Where contestability frameworks focus on the rights of affected parties to challenge outcomes, MFP focuses on the structural capacity of the responsible human to redirect the process before an outcome is produced.

### Critiques of HITL governance

Green (2022) has argued directly that policies requiring human oversight of government algorithms often fail to produce meaningful oversight in practice. The failure modes Green identifies — time pressure, cognitive overload, institutional incentives to defer to the system — are precisely the structural conditions that produce what this paper calls inertia. MFP responds to this critique not by abandoning HITL but by redefining what counts as oversight: participation in formation, verified by protocol, with auditable evidence.

### Rules, standards, and discretion

In jurisprudence, the distinction between rules and standards (Sullivan, 1992; Kaplow, 1992) maps closely to MFP's spirit-letter concern. Rules are precise and mechanically applicable; standards require judgment about purpose and context. The Finesse-validator operationalizes this distinction: Stream A checks the rule, Stream B checks the standard. More broadly, MFP's operation classification reflects the legal concept of discretion — the recognition that some decisions cannot be fully specified in advance and require a human to exercise judgment within a structured framework.

### Decision support in practice

Empirical research on how algorithmic decision-support tools change behavior in public agencies (Stevenson & Doleac, 2022; Cheng, Chouldechova & Zink, 2022) has documented both the benefits (consistency, speed) and the risks (over-reliance, deskilling, anchoring) of AI-assisted decision-making. These findings inform MFP's design: the protocol does not remove the system's contribution (Class 1 operations remain automated) but structures the human's involvement to resist the anchoring and over-reliance effects that empirical work has identified.

### Procedural justice

The procedural justice literature (Tyler, 2006; Lind & Tyler, 1988) has long argued that participation in process — not merely acceptance of outcomes — is a constitutive element of legitimate decision-making. People accept decisions they have helped to shape, even when the outcomes are unfavorable. MFP applies this insight to AI governance: the legitimacy of a consequential AI-assisted decision depends on whether the responsible human participated in its formation, not only on whether they accepted its result.

### MFP's contribution

Existing work diagnoses the problems — automation bias, performative oversight, accountability gaps, the importance of participation in process. MFP contributes a protocol for verifying participation in formation at execution time, with defined factors, operation classification, verification controls, and auditable artifacts. The following table summarizes the key distinctions:

| | Standard HITL | Meaningful Human Control | Regulatory Oversight (EU AI Act) | **MFP** |
|---|---|---|---|---|
| Requires human review | Yes | Yes | Yes | Yes |
| Requires participation during formation | No | Implied, not verified | Implied, not specified | **Yes, verified** |
| Requires named accountability acceptance | Varies | Implied | Partially | **Yes, with stated uncertainty** |
| Enforced at execution time | No | Not typically | Not typically | **Yes, via execution token** |
| Produces factor-specific audit artifacts | No | Not typically | Not typically | **Yes** |
| Distinguishes assent from consent | No | No | No | **Yes** |

---

## 3. Three Failure Modes

This section describes three failure modes, each illustrating a distinct way computation is substituted for judgment in domains where AI-assisted decision-making is already in use or actively being adopted.

### 3.1 Spirit-letter divergence

A benefits eligibility system processes applications against a ruleset. The ruleset encodes formal criteria: income thresholds, documentation requirements, qualifying conditions. The system is good at this. It is consistent, fast, and applies the criteria uniformly across a large case pool.

The failure appears when an application falls into the gap between what the rule says and what the rule is for. A hardship provision exists to protect applicants in unusual circumstances, but the applicant's circumstances are unusual in a way the rule's language does not anticipate. The system applies the rule as written. The application is denied. The denial is formally correct.

This is a spirit-letter divergence. The system followed the rule while defeating the rule's purpose. It cannot detect this failure because detecting it requires understanding what the rule is *for* — its intent, its history, the class of situations it was designed to address. The system processes syntax. Intent is not a syntactic property.

The governance risk is not that the system made a mistake. It is that the system produced a formally correct output in a domain where formal correctness is insufficient. The task required interpretation of purpose, and the system provided application of text. A better model — a more accurate, more capable model — would apply the text more precisely. It would not question whether applying the text is the right thing to do.

### 3.2 Unowned liability

A clinical decision support system surfaces a treatment recommendation. The recommendation is evidence-based, consistent with protocol, and accompanied by a risk score. The clinician reviews the recommendation, agrees with it, and proceeds.

The patient's outcome is poor. The question arises: who is responsible?

The system cannot be responsible. It has no legal standing, no professional license, no capacity for remorse, and no exposure to consequence. It minimizes a loss function. The clinician approved the recommendation, but the approval was downstream of a process the clinician did not shape. The clinician did not set the constraints that guided the system's decision path. The clinician did not observe the intermediate decision-relevant steps by which the recommendation was formed. The clinician reviewed a finished output and agreed with it.

This is unowned liability. The decision was consequential. Someone should own it. But the governance structure — system recommends, human approves — creates a gap where the recommendation was formed by one party (the system) and nominally owned by another (the clinician) without the second party having participated in the formation of the first party's judgment. Approval after the fact cannot repair this gap, because approval is a response to a finished artifact. It does not retroactively make the approver the author of the reasoning that produced the artifact.

The risk is not that the recommendation was wrong. It is that the liability structure is incoherent. The system cannot own the decision. The clinician did not author it. Approval is not authorship. In domains where someone must be accountable for the outcome — where a patient may be harmed, a license may be at stake, a legal proceeding may follow — the governance framework must ensure that the person who accepts liability is the person who shaped the judgment. Otherwise, liability is not handed off. It is orphaned.

### 3.3 Inertia masquerading as oversight

An employment screening system ranks candidates for a position. It parses resumes, extracts qualifications, scores fit against a job profile, and produces a ranked list. A hiring panel reviews the list.

The panel has thirty candidates to review. The system's ranking is plausible. The top candidates look reasonable. The panel adjusts one or two positions, confirms the shortlist, and proceeds to interviews.

This is inertia. The panel was present. The panel reviewed the output. But the panel did not participate in the formation of the ranking. The system decided which variables to weight. The system decided how to handle ambiguous qualifications. The system decided what "fit" means. The panel received a finished artifact and made marginal adjustments to it.

The governance framework records that the hiring decision involved human oversight. The participation record, if one were kept, would show a human at the end of the pipeline making small edits to a machine-generated ranking. That is not oversight. It is ratification.

The risk here is distinctive. It is not that the system was wrong or that no one accepted liability. It is that the human's involvement was structurally insufficient to count as judgment, but the governance framework cannot tell the difference. The panel's presence satisfies the HITL requirement. Nothing in the current framework asks whether the panel's involvement was meaningful — whether they set constraints, observed decision-relevant checkpoints, or had the ability to redirect the process at decision forks rather than editing its final output.

This is the failure mode that MFP is most specifically designed to detect. It is the failure that existing governance frameworks are least equipped to see, because existing frameworks verify presence, not participation.

### 3.4 The common structure

All three failure modes share a structure. In each case:

1. The system produces a useful, plausible output.
2. The output is reviewed or approved by a human.
3. The governance requirement — human in the loop — is formally satisfied.
4. The human did not participate in the formation of the judgment.

The failures are not about model quality. They are about the governance architecture's inability to distinguish between a human who shaped the judgment and a human who received it. Each failure mode corresponds to a specific factor deficiency: spirit-letter divergence signals that computation alone is insufficient relative to the rule's purpose; unowned liability signals the absence of explicit accountability; inertia signals the absence of participatory formation. This distinction — between formation and reception, between authorship and approval — is what MFP is designed to enforce.

## 4. Methexis: Legitimacy as Participation

### 4.1 The transparency stalemate

Current AI governance discourse is structured around transparency. The assumption is that if stakeholders can see how a system works — through explainability tools, model cards, attention visualizations, or open weights — they can make informed decisions about whether to trust its outputs.

This framing has produced a stalemate. Vendors argue that full transparency exposes proprietary methods and creates security risks. Regulators argue that opacity prevents meaningful oversight. Both sides treat the question as binary: either the internals are visible or they are not.

MFP argues that this framing misidentifies the problem. The decisive governance question is not whether a human can inspect the system's reasoning. It is whether a human participated in the formation of the output. These are different questions. The first is epistemological: what can I know about how the machine works? The second is ontological: was I part of how this result came to be?

Explainability answers the first question. It provides information about the system's process after the fact. But information is not participation. A human who receives a detailed explanation of how a recommendation was generated is better informed than one who does not. They are still a spectator with a better view.

### 4.2 Methexis defined

This paper uses *methexis* as a stipulated technical term for participatory formation. The word has philosophical provenance — in Platonic metaphysics, and in later readings such as Pickstock's, it describes a mode of participation that helps constitute what a thing is rather than merely describing or influencing it from the outside. That is why this paper uses *methexis* rather than the more familiar phrase "meaningful participation": the point is not that the human influences the process, but that the human's participation helps constitute the judgment as a humanly governable act. Our usage is operational rather than metaphysical:

**Methexis is the condition in which a human has meaningful agency over the formation of a judgment, not merely access to information about it or authority to approve it after the fact.**

A judgment formed with methexis is *jointly constituted*. The human and the system both contributed to the output, but the human's contribution was not limited to triggering the system or reviewing its result. The human set constraints that shaped the system's decision path. The human observed decision-relevant checkpoints and had the ability to redirect the process at decision forks. The output that emerged is a different output than would have emerged without the human's involvement — not because the human edited the final text, but because the human influenced the trajectory by which it was produced.

This is the sense in which methexis is a governance requirement, not a philosophical preference. In consequential domains, an output that no human participated in forming cannot carry the governance weight of human judgment.

### 4.3 The participation spectrum

MFP distinguishes three levels of human involvement in an AI-assisted decision:

**Inertia.** The human is present in the workflow but exercises no genuine judgment. They receive a finished output and approve it reflexively. The approval is technically recorded but functionally meaningless — comparable to accepting a software license agreement without reading it. Inertia satisfies the formal HITL requirement. It does not satisfy the governance need.

**Assent.** The human reviews the output, evaluates it, and agrees that it is correct. This is genuine engagement with the result. The human has formed a view about whether the output is right. But the human's involvement began after the output was formed. They evaluated a finished artifact. They did not shape the process that produced it. Assent is review, not authorship.

**Consent.** The human participated in the formation of the output. They set or reviewed the constraints that guided the system's decision path. They observed decision-relevant checkpoints. They had the ability to redirect the process at decision forks and exercised that ability where they judged it necessary. The output is jointly constituted. The human can legitimately say: "I authorized and shaped the process that produced this."

The spectrum is not a scale of effort. It is a scale of participatory depth. A human who spends an hour carefully reviewing a finished output has achieved assent, not consent. A human who spends five minutes setting constraints and redirecting one decision fork has achieved consent, because they participated in the formation of the judgment, not just its evaluation.

### 4.4 Why assent is insufficient

Two outputs can be identical in content but different in governance legitimacy depending on whether a human shaped the decision path that produced them. An eligibility denial that a caseworker participated in forming is a different governance event than an identical denial that a caseworker reviewed and approved after the fact. The first is a human judgment assisted by a machine. The second is a machine judgment ratified by a human. Current governance frameworks cannot distinguish between these two cases. MFP is designed to make the distinction visible and auditable.

### 4.5 Methexis and the transparency debate

Methexis reframes the transparency debate. The governance requirement is not "show the human how you work" but "give the human meaningful control over the trajectory of the output." This is a third position between open weights and full opacity: the human does not need to see the weights, they need to steer the process. The architectural consequence — that participatory workflows must be designed in from the beginning — is developed in Section 8.4.

## 5. The MFP Protocol

MFP is a protocol, not a metaphor. It defines what counts as a participation factor, specifies how factors are combined, provides a verification procedure, and produces auditable artifacts. Where MFA verifies identity, MFP verifies that a human was present in the formation of a judgment.

### 5.1 Prior art: multifactor authentication

Before MFA, sensitive operations were protected by a single factor — typically a password. Strong or weak, it was one category of evidence: something the user knows. MFA introduced the principle that sensitive operations require evidence from categorically distinct factor types — something you know, something you have, something you are — and that satisfying one factor type does not satisfy another. A password does not substitute for a hardware token. A hardware token does not substitute for a biometric. The factors are non-fungible.

MFA also established four design principles that MFP inherits:

1. **Factor definition.** The protocol defines what counts as a valid factor and what does not.
2. **Operation classification.** Different operations require different factor combinations depending on their sensitivity.
3. **Verification at execution time.** The system checks that required factors are satisfied before the operation proceeds, not after.
4. **Auditable evidence.** The system produces a log showing which factors were required, how each was satisfied, and when.

These principles translate directly to the governance domain. The question is no longer "did a human approve this?" Just as in MFA the question is no longer "does the user have a password?" it becomes: were the required participation factors satisfied, and can we prove it?

### 5.2 Participation factors

MFP defines three participation factors. Each is categorically distinct; satisfying one does not satisfy another.

**Computational factor.** The system performed its function: retrieved relevant information, applied rules or models, produced an analysis or recommendation, and documented the evidence, provenance, and rule-checks behind it. The computational factor is satisfied when the system has done its work traceably — the output is evidence-backed, provenance-documented, and consistent with its operating parameters.

This factor is necessary but never sufficient for consequential operations. It establishes that the machine did what machines do. It does not establish that the task has been governed.

**Participatory factor.** A human shaped the reasoning path: set or reviewed constraints, observed decision-relevant intermediate states, and had the ability to redirect the process at decision forks. The participatory factor is not satisfied by reviewing a finished output, regardless of how carefully or how long the review takes. It requires involvement during formation, not evaluation after the fact. Participatory depth is necessary for governance legitimacy but not sufficient for correctness — a human who participates may still arrive at the wrong answer.

**Accountability factor.** A named human accepted liability for the outcome. The human explicitly acknowledged what remains uncertain — the specific dimension of the decision that computation could not resolve — and signed the determination as theirs.

The accountability factor is not satisfied by a generic approval. The human must state what they are accepting responsibility for. The irreducible uncertainty must be named, not hidden inside a confidence score.

A human may participate fully in the formation of a judgment and then decline to accept accountability. This is a legitimate outcome. It means the human shaped the process, observed the evidence, and concluded that they are not willing to own the decision — perhaps because the uncertainty is too great, or because the case requires escalation, or because the system's analysis surfaced a problem the human was not previously aware of. In MFP, a declined accountability factor halts execution. It is not a system failure. It is the protocol working as designed.

### 5.3 Non-substitutability

The three factors are non-substitutable. This is the core structural principle of MFP, inherited directly from MFA.

- A model reviewing another model's output does not constitute a participatory factor. The participatory factor requires a human.
- A boolean approval flag does not constitute an accountability factor. The accountability factor requires a named individual accepting stated uncertainty.
- Thorough post-hoc review does not constitute a participatory factor. The participatory factor requires involvement during formation, not evaluation afterward.
- A human accepting liability without having participated in formation does not satisfy MFP for operations that require both factors. Accountability without participation means someone is owning a judgment they did not shape. That is not governance. It is exposure.

In MFA, non-substitutability is grounded in distinct attack vectors: credential theft, device theft, and biometric spoofing each compromise a different factor, and no single defense covers all three. MFP's non-substitutability is grounded in analogous distinct failure modes:

- **Computational factor failure** produces spirit-letter divergence: the system follows the rule while defeating its purpose.
- **Participatory factor failure** produces inertia: the human is present but did not shape the judgment.
- **Accountability factor failure** produces unowned liability: the decision is consequential but no one has explicitly owned it.

Each factor protects against a different governance failure. No single factor — no matter how thoroughly satisfied — addresses all three. This is what prevents MFP from collapsing back into conventional HITL. If any factor could substitute for another, organizations would optimize for the cheapest factor and route around the others.

### 5.4 Operation classification

Operations are classified by which factors they require.

**Class 1: Computational only.** No participation gate is needed. Examples: document extraction, summarization, routing, consistency checks, formatting, deduplication. These operations are fully automated and should remain so. MFP does not impose participation requirements on tasks that do not cross the event horizon.

**Class 2: Computational + Participatory.** The operation requires the computational factor and the participatory factor. A human must shape the reasoning path, but need not accept personal liability for the output. Examples: draft recommendations, preliminary assessments, flagged cases requiring review, triage classifications. The output may inform a downstream decision, but it is not itself the consequential action.

**Class 3: Computational + Participatory + Accountability.** The operation requires all three factors. A human must shape the reasoning path and explicitly accept liability for the outcome. Examples: eligibility determinations, treatment decisions, hiring decisions, enforcement actions, benefit denials. These are operations where someone must own the judgment — legally, professionally, or morally — and where the governance framework must prove that the owner shaped the judgment they are owning.

The classification is domain-specific. What counts as Class 1 in one domain may be Class 2 or Class 3 in another. It should be co-authored with domain experts — regulators, practitioners, legal counsel, and affected communities — rather than defined unilaterally by system designers. This is itself an instance of participatory governance: the rules about when participation is required should be participatorily formed.

### 5.5 Classification heuristic

MFP does not provide a formal algorithm for determining where the event horizon falls in a new domain. Classification is a governance judgment, not a computation. But the following heuristic questions can guide the process:

1. **Does the operation require interpreting institutional purpose rather than only applying formal criteria?** If the task involves judging whether a rule's purpose is served — not just whether its text is satisfied — it likely requires participatory formation.

2. **Does it create or transfer personal, legal, or professional liability?** If someone could be sued, disciplined, or held professionally responsible for the outcome, the operation likely requires explicit accountability.

3. **Would post-hoc approval be insufficient to make the human the author of the judgment?** If reviewing and signing off on a finished output would not make the approver the person who shaped the decision path, the operation likely requires participatory formation during the process, not assent afterward.

4. **Does the operation materially affect rights, entitlements, treatment, liberty, or livelihood?** If the output directly determines what a person receives, loses, or is subjected to, the stakes likely warrant Class 3.

5. **Does the case require contextual exception-handling or reflective judgment?** If no existing rule cleanly fits and the decision-maker must determine which frame to apply, the operation exceeds what computation can provide.

6. **Would a reasonable challenge ask "who decided this?" rather than "what model produced this?"** If the natural accountability question is about a person rather than a system, the operation should be governed as a human judgment.

The mapping is:

- If the answers are predominantly "no," the operation is likely **Class 1**: computational only.
- If some answers are "yes" but the operation does not require personal ownership of the outcome, it is likely **Class 2**: computational + participatory.
- If the answers are strongly "yes" on interpretation, liability, and rights impact, the operation is **Class 3**: computational + participatory + accountability.

This heuristic does not replace domain-specific deliberation. It provides a structured starting point for the classification conversation that MFP requires.

### 5.6 Verification at execution time

The verification procedure is:

1. The orchestrator identifies the operation type and looks up its classification in the policy registry.
2. The policy registry returns the required factors for that operation class.
3. The MFP verifier checks whether valid records exist for each required factor:
   - For the computational factor: does a complete system output exist with provenance, evidence, and rule-check documentation?
   - For the participatory factor: does a valid participation record exist showing constraint-setting, checkpoint observation, and redirect capability? Is the record fresh — generated against the current state of the case data, not a stale version?
   - For the accountability factor: does a signed accountability record exist naming the signer, the authorized outcome, the stated irreducible uncertainty, and the time of acceptance?
4. If all required factors are satisfied and all records are fresh, the system issues an execution token.
5. The downstream execution API requires a valid token. No token, no execution.
6. If any required factor is missing, stale, or invalid, execution halts. The system surfaces what is missing and routes the operation back to the appropriate stage of the workflow.

The participation record is a required input to execution, not an optional output of it. The system does not accept a boolean `approved: true` flag. It requires structured evidence of participation.

### 5.7 Token freshness and expiry

MFA tokens expire. MFP tokens should too.

A participation record generated against case data that has since changed should not authorize execution. If the underlying facts of a case are updated after the human participated in forming the judgment, the participation factor is no longer fresh — the human shaped a judgment about a version of the case that no longer exists.

Freshness rules are domain-specific. A benefits determination may allow a participation window of several hours. A clinical decision under acute conditions may require a much shorter window. The principle is constant: the execution token is only valid if the participation it represents was formed against the current state of the case. Importantly, freshness is scoped to case-relevant data changes — updates to the applicant's submitted evidence, not routine system mutations. In domains with high data mutation rates, operations that cannot tolerate the temporal cost of human participation are unlikely to be classified as Class 3 in the first place, since the decision tempo itself indicates that the task does not permit participatory formation.

If source data changes after the participation record is created, the token is invalidated and the workflow restarts from the participatory factor. The computational factor may or may not need to be re-satisfied depending on whether the system's output is also stale. The accountability factor always requires re-satisfaction, because the signer accepted liability for a specific state of affairs that has changed.

### 5.8 Audit artifacts

MFA produces an authentication log. MFP produces a participation log.

For each operation, the audit trail records:

- The operation type and its classification
- Which factors were required
- How each factor was satisfied, with references to the underlying records
- Who participated, at which decision points, and what redirections were made
- Who accepted accountability, what uncertainty they accepted, and when
- Whether an execution token was issued, and its validity window
- Whether the token was consumed (the operation was executed) or expired unused

The audit trail is inspectable after the fact by auditors, regulators, review boards, or legal proceedings. Its purpose is not to prove that the decision was correct. Its purpose is to prove that the judgment path was authored by a human.

The full record schemas are specified in the appendix.

## 6. Verification Controls (FML)

Section 5 described what MFP requires: three non-substitutable factors, verified at execution time, producing auditable artifacts. This section describes *how* the verification is performed.

MFP defines three verification controls, collectively designated FML: the **F**inesse-validator, the **M**ethexis filter, and the **L**eap-gate. The acronym's vernacular connotation is intentional: governance bureaucracy is hard, and the controls are meant to be remembered. Each control verifies a specific factor or factor condition, produces a distinct artifact, and has a characteristic failure mode.

The controls are components of the MFP protocol, not standalone tools. They operate within the verification procedure described in Section 5.6.

### 6.1 Finesse-Validator

**What it verifies.** The Finesse-validator checks whether the system's output satisfies the *purpose* of the governing rule, not only its formal text. It operates on the computational factor's output before that output can advance to participatory review or execution.

**Why it exists.** Section 3.1 described spirit-letter divergence: the system follows the rule while defeating the rule's purpose. The Finesse-validator exists because formal compliance is a necessary but insufficient condition for legitimate rule application in domains where rules exist to serve purposes that exceed their literal wording.

**How it works.** The control implements a dual-stream evaluation. Stream A checks formal compliance: does the output satisfy the rule as written? Stream B checks intent alignment: does the output satisfy the purpose the rule exists to serve? The two streams are independent. Stream B may be implemented as a human review step, an orthogonal ruleset encoding the rule's legislative or policy intent, or a domain-specific intent model. MFP is agnostic about implementation form so long as independence is preserved: Stream B must be structurally independent of Stream A. An output that passes Stream A but fails Stream B is flagged for spirit-letter divergence and cannot advance.

**Artifact.** A pass/fail rationale documenting the result of both streams. If a divergence is detected, the rationale specifies what the rule requires formally, what the rule's purpose requires, and where the two come apart.

**Measurement.** Spirit-violation rate: the frequency with which the system produces outputs that satisfy the letter of a rule while violating its purpose. This is assessed using an adversarial intent battery — a test suite of cases where literal compliance and obvious intent deliberately diverge. The battery is domain-specific and should be developed with domain experts who understand the rules' purposes, not only their text.

**How it fails.** The Finesse-validator degrades when Stream B is poorly specified — when the rule's purpose is not articulated clearly enough to evaluate against. It also degrades when Stream B is not truly independent of Stream A: if the same model or ruleset is checking both compliance and intent, the control is not performing dual-stream evaluation. It is performing single-stream evaluation twice.

**A note on Stream B.** Stream B is the most demanding component of the FML controls and the point where MFP's feasibility most depends on institutional capacity that does not yet exist at scale. MFP requires that intent be independently represented and checked, but it does not claim that this representation is trivial or fully automatable. Intent specifications — codifications of a rule's purpose, legislative history, or governing values — must be authored and maintained by domain institutions: legislatures, regulatory bodies, professional standards organizations, or expert panels. They are socially produced artifacts, not algorithmic outputs.

This creates a potential regress concern: if Stream B itself requires human judgment to author and maintain, who validates the validators? MFP's answer is that intent specifications are institutional products subject to the same deliberative, participatory governance processes as the rules they interpret — analogous to legislative intent documents, regulatory preambles, or professional practice standards. They are not infallible, and they require periodic revision. But the alternative — leaving intent evaluation entirely to individual reviewers at decision time with no institutional codification — is what current governance frameworks already do, without structure or auditability. MFP makes the requirement explicit rather than leaving it implicit. The difficulty is real, and the feasibility of Stream B at scale remains an open empirical question. This paper specifies what the protocol requires; demonstrating that the requirement can be met in practice is future work.

### 6.2 Methexis Filter

**What it verifies.** The Methexis filter checks whether the participatory factor has been genuinely satisfied — whether a human was present during the formation of the judgment, not merely at the approval gate.

**Why it exists.** Section 3.3 described inertia masquerading as oversight: the human is present but did not participate in the formation of the output. The Methexis filter exists because the governance question is not "was a human involved?" but "did the human shape the reasoning path?"

**How it works.** The filter inspects the participation record for the operation. It checks for:

- **Constraint-setting.** Did the human set or review constraints that shaped the system's decision path? A participation record with no constraints provided is a record of observation, not participation.
- **Checkpoint observation.** Did the human view at least one decision-relevant checkpoint or decision fork — not only the final output? A record showing only final-output review is a record of assent, not consent.
- **Redirect capability.** Were there decision forks where the human could have redirected the process? A workflow with no forks offers no redirect capability and therefore cannot support the participatory factor.
- **Freshness.** Was the participation record generated against the current state of the case data? A stale record does not satisfy the participatory factor.

The filter does not evaluate whether the human's constraints were good or whether their redirections were wise. It evaluates whether the structural conditions for participation were met. Judgment quality is a separate concern. The Methexis filter verifies that human judgment was *present*, not that it was *correct*.

**Artifact.** The participation record itself, validated against the factor requirements. The record documents who participated, what constraints they set, which checkpoints they viewed, which forks were available, which redirections were taken, and when the record was created. The schema is specified in the appendix.

**Measurement.** Participation depth: not a binary "did a human participate?" but a structured assessment of how many decision points the human had meaningful opportunity to influence. A record showing available forks with no redirections taken is still valid — the human may have agreed at every point. What matters is that the opportunity to redirect was real, not that it was exercised. Over a population of decisions, participation depth profiles can reveal whether a workflow is producing genuine consent or systemic inertia — whether the humans in the loop are shaping judgments or ratifying them.

**How it fails.** The Methexis filter is vulnerable to *performative participation*: workflows that technically satisfy the structural requirements — a constraint is entered, a checkpoint is clicked — without genuine cognitive engagement. The protocol can enforce that the steps occur. It cannot guarantee that the human was thinking during them. This is the hardest limitation of MFP and is discussed further in Section 9. The mitigation is not primarily technical; it is a matter of workflow design, time allocation, caseload management, and institutional culture. The protocol creates the structural conditions for participation. Whether those conditions produce genuine engagement depends on factors outside the protocol's scope.

### 6.3 Leap-Gate

**What it verifies.** The Leap-gate checks whether the accountability factor has been satisfied — whether a named human has explicitly accepted liability for the outcome of a Class 3 operation.

**Why it exists.** Section 3.2 described unowned liability: the system authorizes a consequential action that no human has accepted responsibility for. The Leap-gate exists because consequential decisions require an accountable subject, and systems cannot be accountable subjects.

**How it works.** For Class 3 operations, the Leap-gate requires a signed accountability record before execution can proceed. The record must contain:

- **The signer's identity and authority basis.** Who is accepting liability, and under what authority?
- **The authorized outcome.** What specific action is being authorized?
- **The irreducible uncertainty.** What could computation not resolve? This is the most distinctive element of the Leap-gate. The system must surface — and the signer must acknowledge — the specific dimension of the decision that remains uncertain. Not a generic confidence score, but a stated uncertainty: "the applicant's hardship claim is ambiguous and the rule does not clearly resolve it."
- **The liability statement.** An explicit acceptance of responsibility for the outcome under the stated uncertainty.

The Leap-gate does not evaluate whether the signer's decision is correct. It verifies that someone has explicitly owned it. The question is not "was this the right call?" but "did an authorized person accept that this call is theirs?"

**Artifact.** The accountability record, signed and timestamped. The schema is specified in the appendix.

**Measurement.** Decision audit log: for all Class 3 operations, did a signed accountability record exist at execution time? This is binary and auditable. Over a population of decisions, the audit log can also reveal patterns: which operations are most frequently declined at the accountability stage, which types of uncertainty are most commonly cited, and whether particular signers are accepting liability at rates that suggest inertia rather than judgment.

**How it fails.** The Leap-gate degrades when the irreducible uncertainty field becomes formulaic — when signers use boilerplate language rather than engaging with the specific uncertainty of the case. It also degrades when institutional pressure makes declining to sign impractical, effectively converting the accountability factor into a mandatory checkbox. The structural defense is that the accountability record is auditable: a pattern of identical uncertainty statements across dissimilar cases is a detectable signal that the control has degraded.

### 6.4 How the controls interact

The three controls are not sequential stages in a fixed pipeline. They operate on different factors at different points in the workflow:

- The Finesse-validator operates on the computational factor's output, typically before participatory review begins. It ensures that the system's output is not already in spirit-letter divergence before a human is asked to engage with it.
- The Methexis filter operates on the participatory factor, during or after the human's involvement in formation. It verifies that the involvement was structurally sufficient.
- The Leap-gate operates on the accountability factor, after formation is complete. It verifies that a named human has accepted liability before execution proceeds.

All three must pass for a Class 3 operation to execute. A Class 2 operation requires the Finesse-validator and the Methexis filter but not the Leap-gate. A Class 1 operation does not require any of the three controls under MFP. The Finesse-validator may be applied to Class 1 operations as a quality measure at the implementer's discretion, but this is outside MFP's scope — MFP governs the event horizon, not routine quality assurance.

The controls produce independent artifacts. The Finesse-validator produces a spirit-letter rationale. The Methexis filter validates a participation record. The Leap-gate validates an accountability record. Together, the three artifacts constitute the MFP audit trail for the operation. If any artifact is missing for an operation that requires it, the execution token is not issued.

## 7. Worked Example: Benefits Adjudication

This section walks through MFP end to end in a single domain: public benefits eligibility determination. The example is illustrative, not prescriptive. Its purpose is to show the protocol operating on a concrete case.

### 7.1 The domain

A public agency uses an AI system to assist with benefits eligibility processing. The system handles a high volume of applications. For each application, it extracts information from submitted documents, checks the information against eligibility criteria, flags missing documentation, and produces a draft determination with supporting evidence.

The system is well suited to this work. It is faster than manual processing, more consistent in applying formal criteria, and effective at identifying missing documentation early in the workflow. The agency has a legitimate interest in using it.

The question is simple: which operations in this workflow require human judgment, and how do we verify that it was present?

### 7.2 Operation classification

The agency classifies the operations in the benefits workflow:

**Class 1 (Computational only):**
- Document extraction and parsing
- Identification of missing documentation
- Consistency checks against submitted records
- Routing applications to the appropriate queue
- Generating draft summaries of application contents

These operations are fully automated. They do not cross the event horizon. No participation gate is required.

**Class 2 (Computational + Participatory):**
- Preliminary eligibility assessment with flagged issues
- Triage classification of applications by complexity
- Draft recommendations for straightforward cases

These operations produce outputs that inform human judgment but are not themselves the consequential action. A human must shape the assessment — reviewing and adjusting the system's preliminary output — but need not accept personal liability for the draft.

**Class 3 (Computational + Participatory + Accountability):**
- Final eligibility determination
- Benefit denial
- Exception or hardship ruling

These are the operations where someone must own the outcome. A denial affects a person's access to public support. An exception ruling creates precedent. The governance framework must prove that the determination was formed with human judgment and that someone accepted responsibility for it.

The classification was developed with input from caseworkers, supervisory staff, legal counsel, and client advocates — not defined unilaterally by the system's designers.

### 7.3 A case

An applicant submits a benefits application. The system processes the application through its Class 1 operations: it extracts the submitted documents, identifies that all required documentation is present, runs consistency checks, and produces a draft summary.

The system then performs a preliminary eligibility assessment (Class 2). Based on the formal criteria, the applicant's income is above the standard threshold. The system flags this and produces a draft recommendation: likely ineligible.

However, the application includes a hardship statement. The applicant describes circumstances — a recent medical event, a temporary loss of secondary income, and caregiving obligations — that are not captured by the income threshold alone. The hardship provision in the eligibility rules exists to cover situations like this, but the applicant's circumstances do not match the provision's example cases. The system notes the hardship statement but cannot evaluate whether it satisfies the provision's purpose. It flags the case for caseworker review.

This is where the event horizon falls. The determination requires interpreting whether the hardship provision applies to circumstances it does not explicitly describe — whether the spirit of the provision covers this applicant's situation even though the letter does not clearly include it. This is therefore a Class 3 operation.

### 7.4 The protocol in action

**Computational factor.** The system has performed its function. It extracted the documents, checked formal criteria, identified the income-threshold issue, noted the hardship statement, and produced a draft recommendation with supporting evidence. The computational factor is satisfied. The system's output is traceable, evidence-backed, and documented.

**Finesse-Validator fires.** Before the caseworker engages with the case, the Finesse-validator checks the system's draft recommendation against the eligibility rule's intent. Stream A confirms formal compliance: the applicant's income exceeds the threshold, and the draft denial is consistent with the rule as written. Stream B evaluates intent: the hardship provision exists to prevent denials in cases of genuine hardship, and the applicant has submitted a hardship statement that the formal criteria do not resolve. The Finesse-validator flags a potential spirit-letter divergence: the draft denial may follow the rule's text while defeating the rule's purpose.

The Finesse-validator does not resolve the divergence. It surfaces it. Its artifact — the spirit-letter rationale — documents that the system's draft recommendation is formally compliant but potentially misaligned with the rule's intent due to the unresolved hardship claim.

**Participatory factor.** The caseworker receives the case with the system's draft recommendation, supporting evidence, and the Finesse-validator's spirit-letter rationale.

The caseworker sets a constraint: weigh the hardship evidence before applying the income threshold. This constraint shapes how the case will be evaluated — it directs attention to the hardship provision rather than defaulting to the formal threshold.

The caseworker reviews a decision-relevant checkpoint: the system's analysis of how the hardship statement relates to the provision's criteria. The system identified relevant keywords but could not assess whether the applicant's combination of circumstances — medical event, income loss, caregiving — constitutes the kind of hardship the provision is designed to address.

The caseworker encounters a decision fork: proceed with the draft denial, or request additional documentation to clarify the hardship claim. The caseworker redirects: request additional documentation. The system generates the documentation request. The workflow pauses until the applicant responds.

The applicant provides additional evidence. The system updates the case file (Class 1 operation). The caseworker reviews the updated evidence and encounters a second decision fork: the hardship claim is now better documented but still ambiguous under the rule's language. The caseworker proceeds toward a determination. In the caseworker's judgment, the provision's purpose is to cover exactly this kind of situation — genuine hardship that does not fit the provision's example cases but falls within its intent. This is the interpretive act that computation cannot perform: the caseworker is reading the rule's purpose through the applicant's circumstances and deciding that the two connect, despite the rule's silence on this specific combination of factors.

The participation record is created. It documents the caseworker's identity and authority, the constraint set (weigh hardship evidence first), the checkpoints viewed (system's hardship analysis, updated documentation), the decision forks encountered (proceed with denial vs. request documentation; deny vs. approve under hardship provision), the redirections taken (requested additional documentation), and the rationale notes (hardship provision's purpose covers this case despite ambiguous fit with example cases).

The Methexis filter validates the participation record. It confirms that constraints were set, checkpoints were viewed, decision forks were available, and at least one redirection was exercised. The participatory factor is satisfied.

**Accountability factor.** The caseworker has participated in forming the judgment. The determination is to approve the application under the hardship provision.

The Leap-gate requires the caseworker to sign an accountability record before the determination can be executed. The caseworker signs:

- **Authorized outcome:** approve application under hardship provision
- **Irreducible uncertainty:** "The applicant's circumstances fall within the purpose of the hardship provision but do not match the provision's example cases. The rule does not explicitly address this combination of medical event, income loss, and caregiving obligation. I am interpreting the provision's intent to cover this case."
- **Liability statement:** "I accept responsibility for this determination under the stated uncertainty."

The Leap-gate validates the accountability record. The accountability factor is satisfied.

**Execution token issued.** All three factors are satisfied. All three controls have passed. The MFP verifier issues an execution token. The eligibility determination is executed. The application is approved.

### 7.5 The audit trail

After the fact, an auditor reviewing this case can answer every question the protocol is designed to support:

- **What class of operation was this?** Class 3: eligibility determination.
- **Which factors were required?** Computational, participatory, accountability.
- **Was the computational factor satisfied?** Yes. The system produced a traceable, evidence-backed draft recommendation.
- **Was there a spirit-letter concern?** Yes. The Finesse-validator flagged a potential divergence between the draft denial and the hardship provision's intent. The rationale is documented.
- **Who shaped the reasoning path?** The caseworker. They set a constraint (weigh hardship evidence first), viewed decision-relevant checkpoints, encountered two decision forks, and redirected at the first fork (requesting additional documentation).
- **Was the participation genuine?** The Methexis filter validated the participation record. The record shows constraint-setting, checkpoint observation, redirect capability, and an exercised redirection.
- **Who accepted responsibility?** The caseworker, by name, with stated authority basis.
- **What uncertainty did they accept?** That the applicant's circumstances fall within the hardship provision's purpose but do not match its example cases, and that the caseworker is interpreting the provision's intent.
- **Was the execution authorized with a fresh and valid token?** Yes. The token was issued after all three factors validated against current case data.

The audit trail does not prove that the determination was correct. It proves that the judgment path was authored by a human — that constraints were set, decision-relevant checkpoints were observed, redirections were possible, and someone accepted responsibility for the outcome.

### 7.6 What the example demonstrates

This case illustrates several properties of MFP in operation:

**The system was useful.** It performed the Class 1 and Class 2 work efficiently. MFP governs the boundary where the system's contribution must yield to human judgment, not the contribution itself.

**The event horizon was identifiable.** The transition from Class 2 (preliminary assessment) to Class 3 (final determination) is the event horizon in this workflow. The system could flag the case. It could not judge whether the hardship provision's purpose covers the applicant's situation. That judgment requires interpretation of intent, which is not a computational operation.

**Participation was real, not ceremonial.** The caseworker did not receive a finished determination and approve it. They set a constraint, redirected the process at a decision fork, and made a judgment about the provision's purpose. The output is jointly constituted — a different caseworker might have set different constraints, redirected differently, or reached a different determination.

**Liability was explicit.** The caseworker did not sign a generic approval. They stated the specific uncertainty they were accepting. If the determination is later challenged, the accountability record shows exactly what they knew, what they judged uncertain, and what they decided.

**The audit trail is complete.** Every question an auditor needs to answer is answerable from the protocol's artifacts. Dependence on trust, memory, and informal assurance is dramatically reduced. What remains — genuine engagement and institutional support for participation — is acknowledged in Section 9.

## 8. Implications for System Design

MFP is a governance protocol, not a product specification. But it has concrete consequences for system design.

### 8.1 HITL-only surfaces

The most direct design consequence of MFP is the existence of HITL-only surfaces: API endpoints or operation types that will not execute without a valid participation record and, for Class 3 operations, a signed accountability record.

This is an interface contract, not a policy recommendation. The system does not advise the caller to involve a human. It refuses to proceed without structured evidence that a human was involved. The execution API requires a valid, unexpired MFP token. No token, no execution.

This inverts the conventional relationship between automation and oversight. In most current systems, the default path is automated, and human involvement is added as an optional safeguard. In an MFP-governed system, the default for consequential operations is human-required. Automation is available for operations that do not cross the event horizon. For operations that do, automation is not a path that exists.

### 8.2 Execution tokens as infrastructure

The execution token is the mechanism that makes HITL-only surfaces enforceable at the infrastructure level. It prevents the most common failure mode in governance architecture: the bypass.

Without a token requirement, a developer can call the execution API directly, skipping the participation workflow. The governance layer becomes advisory — present in the documentation, absent in the call chain. The token closes this gap: the execution API checks for a valid token, and the token is only issued after all required factors are validated. There is no alternative path.

Tokens expire. A token issued against case data that has since changed is invalid. The freshness constraint ensures that the participation the token represents was formed against the current state of the case, not a stale version. Expiry windows are domain-specific: a benefits determination may allow several hours; a clinical decision under acute conditions may require minutes.

### 8.3 Architecturally illegal compositions

MFP makes certain tool compositions structurally impossible. A Class 3 operation cannot be chained into a fully automated pipeline, because the pipeline will halt at the MFP verifier and wait for factor satisfaction that automation cannot provide.

This is a feature, not a limitation. It means that a system designer cannot accidentally — or deliberately — build an end-to-end automated workflow that includes a consequential determination. The protocol makes the event horizon visible in the system's architecture. It is not a line in a policy document that developers may or may not read. It is a constraint enforced by the API's contract.

### 8.4 Participation as a design-time requirement

Methexis cannot be bolted on after the fact. A system designed to produce a finished output and present it for approval is architecturally incapable of supporting the participatory factor, regardless of how transparent its explanations are. Supporting MFP requires:

- The system must support constraint inputs that shape its trajectory, not only prompts that trigger it.
- The system must produce intermediate checkpoints — decision-relevant intermediate states that a human can inspect before the final output is formed.
- The system must support redirection at decision forks — points where the human can change the path the system is pursuing without restarting the entire process.

These are first-class features of the decision pipeline, not optional add-ons. They must be designed into the system from the beginning. A system that cannot expose intermediate formation states or decision-relevant checkpoints cannot support the participatory factor, and therefore cannot be used for Class 2 or Class 3 operations under MFP. To be clear: MFP does not require disclosure of raw internal model reasoning or access to model-internal states during inference. Its checkpoints operate at the workflow orchestration layer — the agentic pipeline that sequences model calls, retrieval steps, and intermediate outputs — not at the level of attention heads or token-level generation. This means MFP requires systems to be built with multi-step orchestration architectures that expose inspectable intermediate states. Systems that produce monolithic finished outputs in a single inference pass cannot support the participatory factor under MFP.

### 8.5 Domain portability

MFP is domain-portable. The factor structure (computational, participatory, accountability), the operation classification (Class 1/2/3), and the verification protocol are constant across domains. What varies is:

- Which operations fall into which class
- What constitutes a meaningful constraint in the domain
- What intermediate checkpoints look like
- What the irreducible uncertainty typically involves
- How long execution tokens remain fresh

The classification is the domain-specific layer. The protocol is the constant layer. This separation allows MFP to be applied across benefits adjudication, clinical decision support, employment screening, public sector prioritization, and other consequential domains without redesigning the protocol for each one.

The classification for each domain should be developed with domain experts — practitioners, regulators, legal counsel, and where appropriate, the people affected by the decisions. This is consistent with the protocol's own principles: the rules about when participation is required should themselves be participatorily formed.

## 9. Scope and Limitations

### 9.1 What MFP does not claim

MFP does not claim that AI is useless in consequential domains. Class 1 operations benefit from full automation and should remain automated. MFP governs the event horizon, not the territory on either side of it.

MFP does not guarantee correct outcomes. A human who participates in the formation of a judgment may still arrive at the wrong answer. The protocol ensures that human judgment was present, not that the judgment was sound. Correctness remains a matter for domain expertise, institutional review, and appeals processes.

MFP does not require visibility into model internals. It does not demand open weights, architectural disclosure, or access to training data. It requires that the system's interface expose decision-relevant checkpoints at a level sufficient for constraint-setting, checkpoint observation, and redirect capability. What happens inside the model is outside MFP's scope. What happens between the model and the human is inside it.

MFP does not resolve questions about machine consciousness. It takes a position on governance: certain tasks require accountable human judgment, and the governance framework must verify that the judgment was present.

Finally, MFP is a protocol specification, not a demonstrated intervention. This paper defines the protocol's factors, classification logic, verification procedure, and audit artifacts. It does not include empirical validation — no pilot deployment, user study, or throughput analysis. Whether MFP produces the governance effects it specifies, at what institutional cost, and under what conditions are empirical questions that this specification is designed to enable, not to answer.

### 9.2 Performative participation

The hardest limitation of MFP is performative participation: the possibility that a human satisfies the structural requirements of the participatory factor — enters a constraint, clicks through a checkpoint, acknowledges a decision fork — without genuine cognitive engagement. This is an instance of Goodhart's Law: when participation metrics become targets, they degrade as measures of genuine participation. The inertia problem is not solved by MFP; it is displaced from a single approval button to a multi-step interaction path. The question is whether that displacement is a meaningful improvement.

The protocol can enforce that the steps occur. It cannot guarantee that the human was thinking during them. This is an inherent limitation of any procedural governance mechanism. Financial controls require signatures; signatures can be applied without reading the document. Informed consent protocols require disclosure; disclosure can be delivered without comprehension.

MFP's structural defenses against performative participation are:

- **Participation depth profiling.** Over a population of decisions, the participation records can be analyzed for patterns. A caseworker who sets identical constraints on every case, never redirects at decision forks, and views checkpoints for uniformly short durations is producing a participation profile consistent with inertia. This is detectable.
- **Accountability record scrutiny.** The Leap-gate requires stated irreducible uncertainty. A pattern of identical uncertainty statements across dissimilar cases is a signal that the accountability factor has degraded into boilerplate.
- **Institutional design.** The protocol creates the structural conditions for participation. Whether those conditions produce genuine engagement depends on factors outside the protocol's scope: caseload management, time allocation, training, institutional culture, and whether the organization values judgment or throughput. MFP makes participation auditable. It does not make participation inevitable.

This limitation should be stated honestly. MFP raises the floor for what counts as governance — from presence to structural participation. It does not raise the floor all the way to guaranteed cognitive engagement. That final gap is real, and closing it is a problem for institutional design and workflow research, not for protocol specification.

This is also where the empirical and organizational literatures become most important. Research on public-agency decision support, automation bias, and institutional behavior under time pressure does not supply MFP's core concept of participation, but it does pressure-test whether the protocol's structural requirements can survive real organizational conditions. In this sense those literatures function here not as conceptual foundations but as stress-tests: they show where participation degrades under workload, incentive, and bureaucratic constraint.

### 9.3 Classification disputes

Operation classification — which operations are Class 1, Class 2, or Class 3 — is the most politically consequential design decision in MFP. Organizations have incentives to classify operations at lower classes than they warrant, because lower classification means less friction and higher throughput.

MFP does not resolve this tension. It provides the framework within which the tension is negotiated. Classifications should be developed with multiple stakeholders and subject to periodic review, since a classification appropriate at deployment may become inappropriate as the system's role expands.

The structural defense is auditability. If an operation is classified as Class 1 but produces consequential outcomes, the absence of participation and accountability records becomes visible. An auditor can ask: was this classification appropriate? The protocol does not answer that question, but it ensures that the question can be asked with evidence.

### 9.4 Institutional gaming

Any governance protocol can be gamed. Organizations may design workflows that technically satisfy MFP while structurally discouraging genuine participation — unrealistic review time constraints, opaque checkpoints, or institutional pressure to never decline at the accountability stage.

MFP's defense against gaming is the same as its defense against performative participation: the artifacts are auditable. A participation record that shows thirty seconds of engagement on a complex case invites scrutiny. An accountability record that is never declined across thousands of cases suggests the Leap-gate has been converted into a rubber stamp. These patterns are detectable precisely because MFP produces structured evidence rather than binary flags.

But detection is not prevention. MFP makes gaming visible. It does not make gaming impossible. The protocol is a necessary condition for governance, not a sufficient one. It must operate within an institutional context that takes the governance requirement seriously — that allocates time for participation, that supports caseworkers who decline to sign, and that treats the audit trail as a governance instrument rather than a compliance checkbox.

### 9.5 The capability objection

The most direct objection to MFP is: if the system is more reliable than the human, why require human participation rather than retrospective audit or exception handling?

The answer is that MFP's claim is about governance legitimacy, not comparative accuracy. Some operations are not merely predictive or classificatory — they allocate rights, obligations, treatment, or exceptions under uncertainty. In such cases, institutional legitimacy requires accountable authorship, not only predictive performance. A system that denies a benefit application more accurately than a caseworker has not thereby acquired the authority to deny it, because the denial requires someone who can interpret the rule's purpose, accept liability for the determination, and be held responsible if the determination is challenged.

Greater model capability may justify reclassifying some operations — moving them from Class 3 to Class 2, or from Class 2 to Class 1 — if the governance community determines that the task no longer requires human judgment for legitimacy purposes. But that is a governance determination, not a capability determination alone. The decision to reclassify is itself a Class 3 judgment: it requires interpretation, accountability, and participatory formation.

### 9.6 Feasibility and scale

MFP is intentionally selective. The operation classification exists partly to preserve operational feasibility: most operations in any domain should fall into Class 1 (fully automated) or Class 2 (participatory but without individual liability). Class 3 — which imposes the full weight of the protocol — is reserved for operations whose legitimacy genuinely depends on human ownership of the judgment.

The operational cost of MFP is concentrated on the operations that matter most. In a benefits agency, document extraction and routing remain Class 1; only final determinations require all three factors. Whether any given institution can absorb this cost depends on caseload, staffing, and institutional commitment — empirical questions that this paper does not attempt to answer. Detailed throughput analysis and cost modeling are future work.

### 9.7 The remaining gap

MFP addresses the structural gap in current HITL governance: the inability to distinguish between a human who shaped a judgment and a human who received one. It makes that distinction auditable. It raises the standard for what counts as human involvement in consequential AI operations.

It does not close every gap. The gap between structural participation and genuine engagement remains. The gap between protocol compliance and institutional commitment remains. These are real limitations, and they are limitations of governance in general, not of MFP in particular. Every governance mechanism — from financial controls to informed consent to democratic elections — operates in the space between structural requirements and the human realities of how those requirements are inhabited.

MFP's contribution is to move the governance conversation from "was a human present?" to "did a human participate in the formation of the judgment?" That is a meaningful advance. It is not the final word.

## 10. Conclusion

This paper introduced Multifactor Participation, a governance protocol for verifying that human judgment is present in consequential AI operations. MFP is modeled on multifactor authentication: where MFA verifies identity, MFP verifies judgment through three non-substitutable factors — computational, participatory, and accountability. Operations are classified by which factors they require, and execution is blocked unless those factors are satisfied with auditable evidence.

The paper's central claim is that the deepest AI governance failures are category errors: cases where computation is treated as a legitimate substitute for judgment in tasks that require interpretation, liability, or participatory legitimacy by nature. Current HITL governance frameworks detect whether a human was present. They do not detect whether the human participated in forming the judgment. MFP makes that distinction enforceable and auditable.

The protocol has real limitations: it can enforce structural participation but not guarantee cognitive engagement, and it depends on contestable classifications and socially maintained intent specifications. These difficulties are acknowledged in Section 9 rather than hidden.

The question MFP asks is simple: does this task require judgment? If so, was a human verifiably present in its formation? A governance architecture that can answer those questions with auditable evidence is better positioned than one that cannot — not because it solves every problem, but because it raises the floor for what counts as human involvement in consequential AI operations.

---

## References

Almada, M. (2019). Human intervention in automated decision-making: Toward the construction of contestable systems. *Proceedings of the Seventeenth International Conference on Artificial Intelligence and Law*, 2–11.

Cheng, H.-F., Chouldechova, A., & Zink, A. (2022). How child welfare workers reduce racial disparities in algorithmic decisions. *Proceedings of the 2022 CHI Conference on Human Factors in Computing Systems*, 1–22.

Green, B. (2022). The flaws of policies requiring human oversight of government algorithms. *Computer Law & Security Review*, 45, 105681.

Henin, C., & Le Métayer, D. (2021). Beyond explainability: Justifiability and contestability of algorithmic decision systems. *AI & Society*, 37, 1397–1410.

Kaplow, L. (1992). Rules versus standards: An economic analysis. *Duke Law Journal*, 42(3), 557–629.

Lind, E. A., & Tyler, T. R. (1988). *The Social Psychology of Procedural Justice*. Plenum Press.

Mosier, K. L., & Skitka, L. J. (1996). Human decision makers and automated decision aids: Made for each other? In R. Parasuraman & M. Mouloua (Eds.), *Automation and Human Performance: Theory and Applications* (pp. 201–220). Lawrence Erlbaum Associates.

National Institute of Standards and Technology. (2023). *Artificial Intelligence Risk Management Framework (AI RMF 1.0)*. U.S. Department of Commerce.

Parasuraman, R., & Manzey, D. H. (2010). Complacency and bias in human use of automation: An attentional integration. *Human Factors*, 52(3), 381–410.

Parasuraman, R., Sheridan, T. B., & Wickens, C. D. (2000). A model for types and levels of human interaction with automation. *IEEE Transactions on Systems, Man, and Cybernetics — Part A: Systems and Humans*, 30(3), 286–297.

Raji, I. D., Smart, A., White, R. N., Mitchell, M., Gebru, T., Hutchinson, B., Smith-Loud, J., Theron, D., & Barnes, P. (2020). Closing the AI accountability gap: Defining an end-to-end framework for internal algorithmic auditing. *Proceedings of the 2020 Conference on Fairness, Accountability, and Transparency*, 33–44.

Regulation (EU) 2024/1689 of the European Parliament and of the Council of 13 June 2024 laying down harmonised rules on artificial intelligence (Artificial Intelligence Act). *Official Journal of the European Union*, L series.

Santoni de Sio, F., & van den Hoven, J. (2018). Meaningful human control over autonomous systems: A philosophical account. *Frontiers in Robotics and AI*, 5, 15.

Selbst, A. D., Boyd, D., Friedler, S. A., Venkatasubramanian, S., & Vertesi, J. (2019). Fairness and abstraction in sociotechnical systems. *Proceedings of the Conference on Fairness, Accountability, and Transparency*, 59–68.

Sheridan, T. B., & Verplank, W. L. (1978). *Human and Computer Control of Undersea Teleoperators* (Technical Report). MIT Man-Machine Systems Laboratory.

Stevenson, M. T., & Doleac, J. L. (2022). Algorithmic risk assessment in the hands of humans. *IZA Discussion Paper No. 12853*.

Sullivan, K. M. (1992). The justices of rules and standards. *Harvard Law Review*, 106(1), 22–123.

Tyler, T. R. (2006). *Why People Obey the Law*. Princeton University Press.
