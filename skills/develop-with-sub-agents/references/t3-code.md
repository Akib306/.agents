# T3 Code notes

T3 Code supports both native subagents on compatible provider routes and app-owned delegation. Use the active orchestration instructions to choose the route.

## Managed ChatGPT sharing

T3 Code has reported that native Codex forks can fail with `subscription_sharing_unsupported_capability` and may leave the parent conversation unusable. Use app-owned delegation on **Connect with ChatGPT** and when the sharing route is uncertain. If a provider rejects a dispatch, inspect the current diff and report the failure before attempting more work on that route. [T3 Code issue #29992](https://github.com/pingdotgg/t3code/issues/29992) · [Issue #17679](https://github.com/pingdotgg/t3code/issues/17679) · [Prevention PR #28143](https://github.com/pingdotgg/t3code/pull/28143) · [Recovery PR #28962](https://github.com/pingdotgg/t3code/pull/28962)

## App-owned delegation

- Call `orchestrator_capabilities` before the first `delegate_task`. Reuse the selected authenticated provider instance and check that it advertises the model and effort. A catalog entry confirms the supported request shape. The completed task can confirm what ran.
- Send the complete ticket in `delegate_task.task`. Set `target.providerInstanceId`, `target.model`, and the advertised effort under `target.options`. For example, Codex Sol Medium uses `"model": "gpt-6.2-sol"` and `"options": { "reasoningEffort": "medium" }`. Check the provider, model, and effort in the result when reported. Treat a mismatch as a delegation failure. [T3 Code issue #29470](https://github.com/pingdotgg/t3code/issues/29470)
- Use `mode: "wait"` when you need the result in the current turn. If a child is still running, follow the tool's returned `next` instruction.
- Each app-owned `delegate_task` starts a child with the supplied ticket. Fix small review findings in the main thread. For a larger repair that needs an app-owned worker, start a fresh `delegate_task` with the current patch, actionable findings, and acceptance checks.
- When another app-owned review or recheck is required, start a fresh `delegate_task` with the review brief, prior findings, and outstanding objections. For native workers on a compatible route, use the runtime's same-session follow-up.
