---
name: develop-with-sub-agents
description: Orchestrate software development through a main planning/review agent and cost-aware implementation subagents. Use for implementing features, bug fixes, refactors, tests, and multi-file coding tasks when T3 Code orchestration or Codex subagents are available. Select between GPT-6 Luna High, GPT-6.1 Terra Medium or High, and GPT-6.1 Sol Medium using the frozen November 7, 2026 Artificial Analysis benchmarks. Do not use for purely conversational answers, or delegate when no supported subagent runtime exists.
---

# Develop with Sub-Agents

## Objective

Run a **planner → implementer → verifier** development workflow. The **main agent** is responsible for understanding the request, inspecting the codebase, deciding the implementation strategy, choosing the most cost-effective suitable implementation model, reviewing the patch, and reporting the outcome. **Implementation subagents** write the code and run targeted tests.

**Do not let the implementer replace the main agent's planning or acceptance decisions.** Do not select the most powerful worker by default. Select the least expensive worker whose capabilities are appropriate for the task's complexity and risk.

This is an **instruction skill**, not a standalone executable orchestration engine. In T3 Code, it uses app-owned MCP orchestration rather than provider-native agent spawning. Codex-native subagents are permitted only after the connection has been verified to be **non-managed / non-ChatGPT-sharing** and the runtime supports the requested native worker. **T3 Code native delegation currently selects the model, not the exact reasoning effort, in its documented `delegate_task` interface.** Thus the frozen Medium-vs-High cost/benchmark rows are conditional on being able to pin and verify effort through a supported runtime; do not present them as applied when only a model ID was selected.

## T3 Code provider compatibility guard (critical; 2026-11-07)

**Known upstream issue:** T3 Code [#29992](https://github.com/pingdotgg/t3code/issues/29992) documents that Codex native `spawn_agent`/forked sub-agent turns can fail when T3 Code uses **Connect with ChatGPT** (`modelProvider: openai_token_sharing`). The provider returns `subscription_sharing_unsupported_capability` with `param: input`, surfaced as “Codex used a feature that ChatGPT sharing does not support.” A rejected native turn can also poison that conversation so that subsequent text-only turns fail. The exact unsupported wire item is not publicly confirmed; failures may be intermittent. See also [#17679](https://github.com/pingdotgg/t3code/issues/17679), [proposed prevention PR #28143](https://github.com/pingdotgg/t3code/pull/28143), and [proposed session-recovery PR #28962](https://github.com/pingdotgg/t3code/pull/28962). These references are a compatibility warning, not a statement that those PRs have merged.

**Before any delegation:**

1. **T3 Code:** Prefer `orchestrator_capabilities` → `delegate_task` from T3's `t3-code` MCP endpoint, which starts an app-owned child thread without forking the provider-native conversation. Use explicit `providerInstanceId`, `model`, `task`, `role: implementation`, and supported `mode`. This avoids the known *native fork* trigger, but does **not** prove every provider/request type is supported.
2. **Never invoke Codex-native `spawn_agent`, `multi_agent`, `fork`, `send_input`, or a custom `.codex/agents/` worker on a T3 **Connect with ChatGPT** managed-sharing session. Do not enable native agents to get around disabled settings. Under uncertain T3 Codex authentication, treat native agents as unsafe; use T3-owned delegation or no delegation.
3. **Before sending an implementation ticket**, confirm `orchestrator_capabilities` reports an available orchestration adapter and the selected provider/model. Do not interpret `canOrchestrate: true` as proof that the target's authentication route supports every provider-native feature.
4. **If a child fails with provider errors:** Stop spawning further children on that route. Do not automatically repeat the same failed tool call or switch to an unapproved provider/model. Inspect the main thread and current git diff; start a **fresh T3 thread** if the original thread has become unable to accept ordinary messages. Copy only the task summary, constraints, and verified file state into the fresh thread; never assume the failed child's changes succeeded.
5. **Fallback when no working child route exists:** Main agent may implement the smallest safe ticket inline, with the same acceptance tests and review standards, and must explicitly report that delegation was disabled. This is preferable to repeatedly triggering an unrecoverable provider error.
6. **Optional native mode:** For users who need precise `model_reasoning_effort`, only allow native named TOML workers when a separate local Codex CLI/API-key provider route has been verified and a small native-agent probe succeeds. This is **not** a fix for the T3 managed-sharing route. In issue #29992, users reported that disconnecting “Connect with ChatGPT” and reconnecting through the existing CLI login worked; this is a reported workaround, not a universal guarantee.

**Provider/cost guard:** T3 [issue #29470](https://github.com/pingdotgg/t3code/issues/29470) reports that `delegate_task` can switch to an expensive provider/model without user approval. This skill must use only the approved model roster and an expressly selected provider instance; never retry by switching provider or exceeding the requested effort level. T3 currently documents `delegate_task.target` with provider/model selection but does not document an effort field; unverified effort is **not** frozen four-tier enforcement. Provider- and model-level restrictions must be enforced by runtime configuration where possible, not only prompts.

## Frozen model benchmarks

**Snapshot date:** 2026-11-07  
**Source:** Artificial Analysis, Intelligence Index v5.0.1 model pages/comparisons.  
**Freeze rule:** Treat these numbers as immutable routing data. Do **not** silently replace them with live scores, prices, or model rankings. If the user explicitly requests a refresh, propose a versioned update to this file instead.

| Worker | Codex model | Reasoning effort | Intelligence Index ↑ | AA cost/task (USD) ↓ | AA time/task ↓ | Relative use |
|---|---|---|---:|---:|---:|---|
| `impl_luna_high` | `gpt-6-luna` | `high` | 21 | $0.07 | 5.7 min | Smallest well-specified tasks |
| `impl_terra_medium` | `gpt-6.1-terra` | `medium` | 38 | $0.17 | 2.6 min | Default ordinary coding tasks |
| `impl_terra_high` | `gpt-6.1-terra` | `high` | 42 | $0.26 | 4.0 min | Challenging code and nontrivial debugging |
| `impl_sol_medium` | `gpt-6.1-sol` | `medium` | 46 | $0.36 | 4.1 min | Hard multi-step, tool-intensive integration |

Selected domain-specific benchmark figures (higher is better):

| Evaluation | Terra Medium | Terra High | Sol Medium |
|---|---:|---:|---:|
| Terminal-Bench 4.0 | 32% | 42% | 48% |
| FrontierCode 2.0 | 35% | 37% | 33% |
| AutomationBench-AA | 58% | 58% | 63% |

**Interpretation limits:** These are averages across **Artificial Analysis Intelligence Index tasks**, not expected dollar bills, measured performance on this repository, success probabilities, or guarantee of rank order for any coding task. In particular, Terra High is **above** Sol Medium on FrontierCode 2.0 despite Sol's higher overall Intelligence Index. Actual cost and speed depend on task shape, context, provider, caching, account limits, and retries. In subscription-based Codex, published dollar figures are comparative signals, not necessarily direct account charges.

**Benchmark sources (fixed reference URLs):**

- Luna High: https://artificialanalysis.ai/models/gpt-6-luna-high
- Terra Medium vs. Terra High: https://artificialanalysis.ai/models/comparisons/gpt-6-1-terra-high-vs-gpt-6-1-terra-medium
- Terra High vs. Sol Medium: https://artificialanalysis.ai/models/comparisons/gpt-6-1-terra-high-vs-gpt-6-1-sol-medium
- Terra Medium vs. Sol Medium: https://artificialanalysis.ai/models/comparisons/gpt-6-1-terra-medium-vs-gpt-6-1-sol-medium
- Codex subagents: https://learn.chatgpt.com/docs/agent-configuration/subagents
- Codex skills: https://learn.chatgpt.com/docs/build-skills

## Roles and responsibilities

### Main agent — planner, router, integrator, verifier

1. Interpret the user's request and discover relevant repository conventions and constraints.
2. Inspect enough code to understand relevant control flow, interfaces, dependencies, and tests.
3. Produce a bounded implementation plan with success criteria and file ownership.
4. Split the plan into independently verifiable implementation tickets where helpful.
5. Choose and dispatch the appropriate implementation worker **per ticket** using the frozen routing policy.
6. Inspect each resulting diff; test its claims; integrate dependent changes; identify regressions.
7. If necessary, send a precise follow-up ticket or escalate to a stronger worker.
8. Deliver a concise final summary: changes, tests, limitations, and worker choices.

Do not turn the main agent into an additional implementation worker merely to avoid delegation, except for trivial glue edits, tooling fixes, **a provider-compatibility failure**, or when no safe delegation route is available. Never report a subagent's claims as verified without checking them.

### Implementation worker — scoped code changes

- Accept the main agent's ticket and implement **only its authorized scope**.
- Read relevant code and follow local `AGENTS.md`, style, test, and security requirements.
- Make minimal changes and add or adjust tests when appropriate.
- Run the cheapest useful targeted validation available; describe any tests not run.
- Report changed files, behavioral effect, tests and their results, risks, and open questions.
- Do not silently redesign requirements, widen scope, overwrite unrelated work, commit, push, or perform irreversible operations.
- If blocked by missing information, return a concrete blocker to the main agent.

## Frozen routing policy

Choose by **task fit first, benchmark cost second**. Use this deterministic decision sequence:

1. **Break down the request.** A large feature is not automatically a Sol task: its small, independent tickets may be assigned to Luna or Terra.
2. **Assess risk.** Mark the ticket **high-risk** if it touches authentication, authorization, cryptography, financial transactions, irreversible migrations, concurrency, distributed coordination, or security boundaries, or if a wrong implementation is difficult to detect. High risk increases review rigor; it is not a reason to skip tests.
3. **Pick the lowest suitable tier** from the four tiers below. Favor the cheaper model on ties. Do not calculate fake per-task success probabilities from the Intelligence Index.
4. **Escalate** if verification fails for nontrivial reasons, a worker cannot resolve the issue within one targeted repair attempt, or the scope proved materially more complex than planned.
5. **Record the selection** as `worker — reason — frozen intelligence/cost signal` in the task handoff or final summary.

### Tier L — `impl_luna_high` ($0.07/task index)

Use when **all** apply (and the actual model/effort is available):

- Clear specification and acceptance criteria.
- Localized edit with a known pattern or an obvious implementation path.
- Small blast radius; no new architecture or subtle system invariants.
- Easy to verify automatically.

Examples: a precise one-file bug fix, adding a straightforward field, boilerplate tests, obvious CLI help text, mechanical renames with bounded references. **Do not** use Luna for a vague request simply because the number of changed lines appears small.

### Tier M — `impl_terra_medium` ($0.17/task index; default)

Use for ordinary development that requires normal repository understanding, moderate reasoning, and typical tests: simple endpoints, components, data transformations, modest refactors, and well-bounded multi-file changes. It has a higher Intelligence Index than Luna (38 vs. 21), lower AA mean time/task (2.6 vs. 5.7 minutes), and remains below Terra High/Sol on cost/task.

### Tier H — `impl_terra_high` ($0.26/task index)

Use for complex algorithms, demanding code reasoning, subtle bugs, difficult refactors, framework interactions, flaky tests, and code-heavy tasks that benefit from deeper deliberation. Prefer this tier over Sol Medium for **primarily code-centric** challenges unless a concrete reason favors Sol: on the frozen **FrontierCode 2.0** benchmark, Terra High scores **37% vs. Sol Medium's 33%**, at a lower mean cost per benchmark task.

### Tier S — `impl_sol_medium` ($0.36/task index)

Use for difficult cross-system or tool-intensive work involving many interacting constraints, ambiguous integration behavior, complex debugging across boundaries, difficult environment/tool orchestration, and tasks where stronger broad reasoning is likely to avoid costly rework. Sol Medium leads Terra High on the frozen overall Intelligence Index (46 vs. 42), Terminal-Bench 4.0 (48% vs. 42%), and AutomationBench-AA (63% vs. 58%). Choose it for a concrete need, **not** simply because it is more expensive.

### Escalation / fallback ladder

- Start with the selected available tier. For native T3 delegation without effort control, collapse Terra Medium/High into the unverified-effort Terra model rather than pretending they are distinct workers.
- For an implementation/test failure, make **at most one targeted repair attempt on the same tier** if the cause is clear and localized.
- If the failure suggests reasoning or integration weakness, escalate: Luna → Terra Medium → Terra High → Sol Medium. Skip tiers when a known domain signal justifies it (for example, tricky algorithmic issues → Terra High; complex terminal workflows → Sol Medium).
- If Terra High fails on a pure code task, reassess the plan, requirements, and tests **before** escalating to Sol; Sol's overall index does not guarantee better pure-code results.
- If Sol fails, stop automatic escalation; the main agent diagnoses and reports unresolved blockers or asks for an authorized alternative.
- Never silently fall back to an unlisted model or reasoning level. For T3 Code, do not assert an effort that the runtime did not establish. If a configured worker is unavailable, choose the next **available suitable** listed tier and disclose the change; if none are available or the provider rejects delegation, allow an explicitly disclosed inline main-agent implementation fallback without retrying unsupported native calls.

## Required orchestration workflow

### 1. Plan

The main agent should create a compact plan before delegating:

```text
Goal:
Existing behavior / relevant architecture:
Constraints and non-goals:
Implementation tickets, dependencies, and file ownership:
Acceptance criteria / tests:
Risks and rollback considerations:
```

For an easy task, one ticket and a 2–4 line plan are sufficient. For larger changes, create a dependency order and independent tickets. Do not delegate an unbounded goal like “implement everything” without scope or checks.

### 2. Route and dispatch

For every ticket, write a handoff in this format:

```text
TICKET: <short identifier>
WORKER: <impl_luna_high | impl_terra_medium | impl_terra_high | impl_sol_medium>
ROUTING RATIONALE: <task features + why least expensive suitable worker>
OBJECTIVE: <one clear outcome>
FILES/OWNERSHIP: <paths or module boundaries allowed to change>
CONTEXT: <existing interfaces, relevant files, patterns, constraints>
IMPLEMENTATION STEPS: <ordered guidance; leave local details to worker>
ACCEPTANCE CRITERIA: <observable conditions>
VALIDATION: <tests/type checks/lint or manual verification>
DO NOT: <out-of-scope edits, risky operations, unapproved dependencies>
RETURN: <file list, summary, tests/results, risks, blockers>
```

Dispatch using the active supported runtime. **In T3 Code, use its `orchestrator_capabilities` → `delegate_task` flow** described below, with the model ID shown as available by the tool. Native Codex agents are **forbidden** on T3-managed ChatGPT sharing even when Codex exposes the native agent tools. Consider native agents only with a verified non-managed/CLI/API-key route and a successful compatibility probe. **Do not pretend a model or effort was selected unless the actual subagent runtime confirms it.** A prompt instructing a worker to “think high” is not equivalent to setting reasoning effort.

### 3. Parallelism

- Run independent tickets in parallel **only** when they do not write overlapping files or dependent interfaces.
- Specify exclusive file ownership. Prefer separate working trees if your environment uses them.
- Run dependent tasks sequentially and verify upstream interfaces before dispatching downstream work.
- Keep concurrency modest; more agents consume more tokens and can increase integration overhead.
- Only the main agent merges or accepts work across boundaries.

### 4. Validate and review

After each worker returns, the main agent must:

1. Inspect the actual changed files/diff; check for unintended edits and requirements drift.
2. Evaluate correctness, edge cases, security, compatibility, and missing tests.
3. Run relevant checks, or state explicitly why they cannot run.
4. Compare results to the ticket's acceptance criteria, not the worker's confidence.
5. Decide **accept**, **targeted repair**, **escalate**, or **blocked**.

Treat a failed test as evidence to investigate, not an automatic signal to jump to the most expensive model. Avoid rewriting working code without a measured need.

### 5. Report

At completion, summarize:

```text
Implemented: <observable behavior and changed files>
Delegation: <ticket → worker; brief reason>
Verification: <checks run and pass/fail status>
Remaining issues: <explicit limitations, if any>
```

Don't imply the whole request is complete when only part passed verification. Never fabricate tests or model usage.

## T3 Code setup and actual routing

**Project installation** (recommended):

```text
<repository>/.agents/skills/develop-with-sub-agents/SKILL.md
```

In T3 Code select a provider capable of running subagents, open the project, restart the agent session after adding the skill (command palette → **Restart agent session**), and invoke `$develop-with-sub-agents` or choose the skill from the composer. Confirm it appears for the selected provider. If a provider does not discover this path, install in that provider's documented skills directory instead; T3 shows only skills discovered by the provider/environment.

### Preferred T3 Code V2 delegation

1. Call **`orchestrator_capabilities`** before routing. Identify the actual authenticated provider instance, `providerInstanceId`, supported model IDs, and whether child tasks are available. Search the model catalog through the capabilities tool if a model is omitted from its compact initial listing.
2. Resolve each selected tier to an actual supported model and provider instance. Use the benchmark map below as the target, not as proof of runtime availability.
3. For each ticket, call **`delegate_task`** with `task` equal to the **complete** ticket and `target` containing `providerInstanceId` plus the exact supported `model`. Set `role` to `implementation`. Use `mode: "wait"` for dependent work or `mode: "async"` for independent work; inspect the result with `task_status` as needed. Use only documented tool arguments.
4. Verify the returned `providerInstanceId`, `model`, task ID and terminal result. Child agents do **not** receive the entire parent conversation. Put all file boundaries, interfaces, success criteria and tests in `task`. Verify the actual patch and tests yourself.
5. If orchestration fails with `subscription_sharing_unsupported_capability` or makes the thread unusable, do not repeatedly retry or silently invoke native Codex agents. Preserve repository state, switch to a fresh thread if needed, and follow the provider compatibility guard above. If orchestration is unavailable or the selected model is not advertised, do not fabricate delegation. Choose the next available suitable **approved** model from this frozen roster, or report the blocker. Do not silently switch to another provider or expensive model.

**Native T3 `delegate_task` target map** (model IDs must be confirmed via `orchestrator_capabilities`):

| Frozen worker | `target.model` | Requested reasoning | Enforceable using documented `delegate_task` alone? |
|---|---|---|---|
| `impl_luna_high` | `gpt-6-luna` | high | Model yes; effort not explicitly |
| `impl_terra_medium` | `gpt-6.1-terra` | medium | Model yes; effort not explicitly |
| `impl_terra_high` | `gpt-6.1-terra` | high | Model yes; effort not explicitly |
| `impl_sol_medium` | `gpt-6.1-sol` | medium | Model yes; effort not explicitly |

**Critical effort limitation:** In the documented T3 Code V2 `delegate_task` schema, the `target` accepts `providerInstanceId`, `driverKind`, and `model`, but **no reasoning-effort field**. Therefore, direct T3 delegation cannot, by that interface alone, distinguish Terra Medium from Terra High or guarantee Luna High/Sol Medium. When effort cannot be pinned, label the assignment by *model only* (`terra / effort unverified`); its exact frozen AA row is a **reference**, not an observed runtime setting. Do not assert an exact expected AA cost/task for unverified effort. Explicitly tell the user if exact-effort routing is important.

**Correctness-first simplified routing for T3 native delegation without effort control:**

- For tiny, fully specified changes, choose `gpt-6-luna` only if the provider's actual default effort/capability is suitable; otherwise choose Terra.
- Default to `gpt-6.1-terra` for ordinary changes and deep code-focused tasks; do not claim a Medium/High distinction.
- Use `gpt-6.1-sol` for complex cross-system/tool-heavy tasks, when it is the least costly suitable option based on the frozen ranking and actual execution characteristics.
- An unavailable target or failed worker must be reported or escalated explicitly; never quietly re-delegate onto a different premium/pro model.

**Tool call shape** (illustrative syntax only; use the actual tool, not a shell command):

```json
{
  "task": "TICKET: auth-callback-test\nOBJECTIVE: Add a regression test for the specified callback behavior.\nFILES/OWNERSHIP: tests/auth/callback.test.ts only\nACCEPTANCE: test passes; no production-code changes\nRETURN: files changed, test command/results, blockers",
  "target": {
    "providerInstanceId": "<provider-instance-id-from-orchestrator_capabilities>",
    "model": "gpt-6.1-terra"
  },
  "role": "implementation",
  "mode": "wait"
}
```

The placeholder must be replaced with an **observed** provider instance ID, not a guessed ID. Do not paste JSON into the chat expecting it to spawn an agent; the parent must invoke the real orchestration tool.

### Alternative: exact reasoning levels via Codex-native custom subagents

Only when the parent uses a **verified non-managed Codex CLI/API-key connection**, native subagent spawning has been probed successfully, and T3 is **not** routing through Connect with ChatGPT, define four agents as TOML under `.codex/agents/` (project) or `~/.codex/agents/` (global). Ask the parent to spawn the **named native agent**. This is the route that can pin `model_reasoning_effort` as specified. **T3-owned `delegate_task` does not automatically use those TOML files or inherit their per-agent reasoning settings.** Native subagent availability and exposure inside T3 must be verified in the actual installation.

**`.codex/agents/impl_luna_high.toml`**

```toml
name = "impl_luna_high"
description = "Implements tightly scoped, low-risk, easily verifiable coding tickets."
model = "gpt-6-luna"
model_reasoning_effort = "high"
developer_instructions = """
You are an implementation worker, not the planner. Execute only your assigned ticket.
Follow existing project conventions. Keep patches small and focused. Add or run
relevant tests. Never widen scope, commit, push, or overwrite unrelated work.
Return changed files, test results, blockers, and any concerns.
"""
```

**`.codex/agents/impl_terra_medium.toml`**

```toml
name = "impl_terra_medium"
description = "Default implementation worker for standard features, fixes, and refactors."
model = "gpt-6.1-terra"
model_reasoning_effort = "medium"
developer_instructions = """
You are an implementation worker, not the planner. Implement the bounded ticket,
respect file ownership and repository conventions, and avoid unrelated edits.
Add or update relevant tests and run targeted validation. Do not commit or push.
Return changed files, verification results, unresolved risks, and blockers.
"""
```

**`.codex/agents/impl_terra_high.toml`**

```toml
name = "impl_terra_high"
description = "Deep code-reasoning worker for algorithms, subtle debugging, and difficult refactors."
model = "gpt-6.1-terra"
model_reasoning_effort = "high"
developer_instructions = """
You are an implementation worker for a difficult but bounded coding ticket.
Trace invariants and failure modes before changing code. Keep edits within the
assigned ownership boundary. Create regression tests where feasible. Report
assumptions, tests, remaining risks, and files changed. Do not commit or push.
"""
```

**`.codex/agents/impl_sol_medium.toml`**

```toml
name = "impl_sol_medium"
description = "Complex integration and tool-intensive implementation worker."
model = "gpt-6.1-sol"
model_reasoning_effort = "medium"
developer_instructions = """
You are an implementation worker for complex integration tickets. Establish
assumptions and dependency boundaries, investigate relevant system interactions,
and implement only the approved ticket. Validate with realistic tests. Never
silently expand scope or run irreversible operations. Do not commit or push.
Report changed files, commands/tests, risks, and blockers clearly.
"""
```

Optional `.codex/config.toml` (merge with existing config):

```toml
[agents]
enabled = true
max_concurrent_threads_per_session = 4
```

If Codex-native agents are unavailable or unsafe (including managed ChatGPT sharing), use T3-owned `delegate_task` with the effort limitation noted above. If T3 delegation also fails, use the explicitly disclosed main-agent fallback or stop; do not rerun failed native requests. If **exact** frozen four-tier routing is a hard requirement, stop rather than silently pretending it is enforced.

### References for runtime behavior

- T3 Code orchestration interface: https://github.com/pingdotgg/t3code/blob/main/docs/orchestration-v2/orchestrator-mcp-server.md
- T3 Code skills and model picker: https://github.com/pingdotgg/t3code/blob/main/docs/user/composer.md
- Codex custom agents: https://learn.chatgpt.com/docs/agent-configuration/subagents

## Non-negotiable rules

- The main agent owns architecture, planning, worker selection, integration, and final acceptance.
- Workers own only assigned implementation tickets.
- Benchmarks stay frozen to the snapshot in this file until explicitly updated.
- Cost is optimized **subject to capability and risk**, not at the expense of correctness.
- Use domain-specific benchmark signals where relevant; do not blindly sort by Intelligence Index.
- Do not delegate secrets, credential extraction, or unauthorized operations.
- Do not perform destructive operations or production deployments without authorization.
- Never invent a successful spawn, model selection, reasoning effort, patch, benchmark score, or test result.
