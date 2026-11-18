---
name: develop-with-sub-agents
description: Plan, delegate, and verify coding work using subagents in Codex, GitHub Copilot, T3 Code, or another runtime that supports delegation. Use for features, fixes, refactors, and tests that benefit from scoped implementation tickets and a bounded review loop.
---

# Develop with Sub-Agents

The **main agent** is the agent the user interacts with directly. It uses the model and reasoning effort configured for the user's conversation. It owns the plan, worker selection, integration, verification, final acceptance, and communication with the user.

Implementation subagents own scoped tickets and run targeted checks. The main agent can review directly or delegate to a separate reviewer where independent review is needed.

## Choose a delegation route

Use the active runtime's supported subagent interface. Check whether it can select a model or effort, resume a worker, and isolate concurrent edits. In Codex or a GitHub Copilot surface with subagents, use its built-in delegation. For T3-managed sessions or app-owned delegation, consult the optional [T3 Code notes](references/t3-code.md).

Reuse the authenticated session and its approved provider across tickets. When delegation is unavailable or unsuitable, implement inline with the same acceptance criteria and disclose the fallback.

## Plan and delegate

1. Inspect the relevant code and repository instructions. Define the outcome, acceptance checks, scope, and file ownership. Identify dependencies and risks that need closer review.
2. Choose the least costly suitable worker from the available approved options. Use the OpenAI routing table below where applicable. Match the worker to the ticket's scope, difficulty, and risk.
3. Give each worker a self-contained ticket with the objective, owned files, relevant interfaces and conventions, acceptance criteria, validation commands, and any limits on edits or side effects. Ask for the patch summary, check results, and remaining risks.
4. Run independent tickets in parallel only when their edits and interfaces are independent. Use isolated workspaces when appropriate. Sequence dependent changes and verify upstream interfaces before dispatching the next ticket.

Give workers only the information and permissions needed for the ticket. Keep secrets out of handoffs. Follow the user's authorization for commits, external actions, and destructive operations.

## Review and repair

1. Inspect the actual diff, compare it with the acceptance criteria, and run the relevant checks. Review correctness, edge cases, regressions, and risks appropriate to the change.
2. If repairs are needed, resume the **same implementation subagent** using its saved handle or thread when the runtime supports follow-ups. Send only the actionable findings, the affected files or checks, and any new constraints. If an existing independent reviewer is needed again, reuse that reviewer where the runtime permits it. Retaining the conversation gives each worker access to its earlier context and can reuse eligible cached input.
3. Recheck the revised diff and rerun affected checks. Default to **one initial review and at most two delegated repair-and-recheck rounds per ticket**. Stop early when the checks pass or a concrete blocker prevents progress. Escalation to a stronger worker uses the same repair budget.
4. If the runtime requires a fresh worker for a round, keep the approved model and effort where suitable and send a compact handoff with the current patch, prior findings and decisions, and remaining checks.
5. After the final delegated recheck, the main agent may resolve a localized issue inline and verify the fix. Report any unresolved issue and its impact.

## Frozen OpenAI subagent routing

Use this roster to select models and reasoning effort for delegated subagents.

Updated 2026-11-17 from the supplied screenshots of Intelligence Index v5.0.1 and Cost per Intelligence Index Task. Refresh only at the user's request. [Artificial Analysis](https://artificialanalysis.ai/)

| Worker | Model | Effort | Intelligence Index | AA cost/task (USD) | Typical use |
|---|---|---|---:|---:|---|
| `impl_luna_high` | `gpt-6-luna` | `high` | 21 | $0.07 | Small, well-specified edits that are easy to verify |
| `impl_luna_xhigh` | `gpt-6-luna` | `xhigh` | 23 | $0.10 | Localized tasks that need more deliberation |
| `impl_terra_high` | `gpt-6.1-terra` | `high` | 42 | $0.26 | Default for ordinary development and code-heavy work |
| `impl_sol_medium` | `gpt-6.2-sol` | `medium` | 53 | $0.41 | Difficult cross-system or tool-intensive integration |

The only approved Sol worker is GPT-6.2 Sol at `medium` effort. Require a supported way to set or confirm that effort. Use another suitable option or work inline if the runtime cannot honor an explicit model, effort, or cost constraint.

When a runtime has a different catalog, use its approved models or its standard worker if that choice satisfies the user's constraints. Report the selection the runtime exposes, including whether settings were explicit, inherited, or unverified. Compare the table's benchmark averages when choosing among those exact configurations. Use repository evidence and domain-specific benchmarks where available.

If a ticket needs more capability, reassess the plan and go to the next suitable tier. The OpenAI escalation order is Luna High → Luna XHigh → Terra High → Sol Medium. Skip tiers that cannot meet the ticket's needs.

## Report

Summarize the outcome, worker choices, checks and results, and any unresolved issues. Report context reuse when an existing worker resumed. Cite cache hits only when the runtime reports them.
