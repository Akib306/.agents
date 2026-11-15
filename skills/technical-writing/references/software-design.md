# Software design documents

Help readers assess an engineering decision. Ground the document in the supplied requirements and current system. When source code or existing project decisions are available, inspect the relevant evidence before describing behavior. Distinguish verified current behavior, the proposal, assumptions, and open questions.

## Choose the artifact

- **Design doc or RFC:** Explain a proposed change and invite assessment of its mechanics and trade-offs.
- **ADR:** Record a specific decision, its context, status, alternatives, and consequences. Preserve established location, naming, and lifecycle conventions. A proposal is not an accepted decision.
- **Technical specification:** Define observable behavior, contracts, constraints, and acceptance criteria precisely enough to implement or verify.
- **Overview:** Explain the existing system. Use the explanation guidance when no decision is being proposed.

Follow the project's template when one exists. Add only sections that help evaluate this change; a small decision may need a few paragraphs. The existing `documentation-and-adrs` skill can supply project documentation conventions when that separate work is needed; it is not a prerequisite for editing prose.

## Make the decision reviewable

Lead with the concrete problem and the proposed behavior, then show why the proposal fits. A useful document lets the reader answer:

- What is happening now, who is affected, and what outcome is required?
- Which constraints matter: compatibility, scale, latency, cost, operational capacity, data ownership, or delivery conditions?
- How do components and data move through the proposed path? What changes at their boundaries?
- What happens during failure, retry, concurrency, recovery, and partial completion where relevant?
- Which credible alternatives were considered, including retaining the current system? Why do they fit less well under these constraints?
- What is the cost or compromise of the choice, and which unresolved question could change it?

Use a small request, event, or data example to make behavior concrete. Label invented examples as illustrative. An example should expose a contract or decision, not decorate the page. A diagram earns its space when it clarifies a flow or boundary that prose would obscure.

## State mechanics and evidence precisely

Name ownership, inputs, outputs, state transitions, and failure behavior at the level the reader needs. Define what “retryable,” “durable,” “consistent,” or “real time” means in this system. Replace “scalable” or “robust” with a supported bound or the concrete mechanism; if the bound is unknown, say so.

Keep measured, estimated, and target values distinct. Do not turn a performance target into a benchmark result. Keep `must`, `should`, and `may` distinct when they express requirements. Do not promote assumptions into guarantees, a planned integration into a shipped feature, or a draft decision into an accepted one.

For alternatives, compare the same criteria rather than giving the preferred option benefits and the others only drawbacks. Record real trade-offs without creating straw alternatives or justifying a decision retroactively with invented constraints.

## Address delivery and human effort where relevant

For an implementation proposal, cover validation, rollout, compatibility, observability, migration, and rollback or recovery only to the depth the change needs. Surface a genuinely irreversible step or an unavailable reversal rather than promising a generic rollback. Do not invent owners, dates, cost estimates, or consensus.

For a proposed operator or user workflow, walk through the full sequence. Count login and MFA prompts, redundant commands, repeated manual inputs, and context switches. Reuse existing authenticated sessions and batch remote work where supported. Explain unavoidable repeated authentication before recommending the workflow. Technical correctness does not excuse unnecessary user effort.

## Edit without redesigning

Preserve interface names, invariants, defaults, units, compatibility promises, command semantics, security boundaries, and decision status. If something appears incorrect, state the issue and its evidence or mark it unresolved; do not silently change the design while making the prose smoother.

A final reader pass should establish whether an engineer can explain the proposed path, evaluate its trade-offs, and identify what remains undecided. Remove repeated background and implementation detail that does not affect that assessment.
