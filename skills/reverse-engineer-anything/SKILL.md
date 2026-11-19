---
name: reverse-engineer-anything
description: Use REA on a selected binary, package, capture, or app when the user explicitly requests REA or invokes this skill.
metadata:
  version: "49"
  tool_count: "229"
---

# Reverse Engineer Anything

Use this workflow only when the user explicitly requests REA or invokes `$reverse-engineer-anything`. Start with the supplied target and question. Resolve a named target when it is unambiguous, and ask if the requested artifact or runtime remains unclear.

## Choose the target and guide

Use the current REA tool schema. `open_binary` binds active-target workflows. Target-free calls take their own path or endpoint.

| Target or question | First step |
| --- | --- |
| Executable, library, managed assembly, package, firmware, or static format | Read the matching section in [native and artifact workflows](references/native-and-artifacts.md). Use `open_binary` for active-target native and archive analyses. |
| Electron ASAR or extracted JavaScript | Use `analyze_javascript_application`. Read [JavaScript workflows](references/javascript-applications.md) for module and feature questions. |
| Android APK method, class, or declaration | Use `inspect_android_package`. See [Android workflows](references/android-applications.md). |
| Browser, Electron, or native runtime, or a saved traffic or signal capture | Choose the focused workflow in [runtime observation](references/runtime-observation.md). Declare any requested launch, attachment, or actions before execution. |
| AgentEnv bundle | Read [agent environments](references/environments.md) before recording or exporting. |
| Exact comparisons, retained results, or incomplete views | Read [evidence workflows](references/evidence-workflows.md). |

Use an available connection directly. Read [connection and recovery](references/connection-and-recovery.md) for an observed setup, availability, transport, or CLI blocker. Follow the active client's permissions for access, execution, installations, configuration, and effects.

## Work from focused evidence

- Use the smallest useful inventory or default summary. For large JavaScript or ELF layout analyses, request summary delivery first. Carry the returned `parent_evidence_id` into focused `inspect_analysis_view` requests or retained-evidence comparisons. Read the complete record only when needed.
- Reuse matching sessions and existing Evidence. If a reply is truncated or exceeds the transport limit, query a precise retained view or export the complete record. Avoid repeating an identical analysis or a rejected call without a changed input or resolved blocker.
- Investigate broader questions in stages. Trace the relevant entry point and state changes. Use runtime evidence when a static result cannot establish the requested behavior and the user has authorized that runtime work.
- Cite Evidence IDs and distinguish observations, inferences, and unknowns. Report coverage and limitations. Close native sessions opened for the investigation after retaining any evidence needed for the result.
