---
name: impeccable
description: Design or substantially refine a frontend UI. Use for new surfaces, visual redesign, UX critique, or explicit Impeccable commands.
metadata:
  version: 4.5.2
---

# Impeccable

Honor the brief and the current design. Identify the user's goal on the surface:

- **Persuade:** visitors decide and act.
- **Operate:** users complete a task.
- **Read:** readers find and understand information.
- **Experience:** the artifact itself is the focus.

## Route the task

- For an explicit or clearly implied Impeccable command, open only its playbook in the [command index](reference/routing.md#command-index). Use the native variant when it applies.
- For a new UI or visual redesign, open [new work](reference/new-work.md). Use [init](reference/init.md) when the project needs new product context. Read the [craft floor](reference/craft-floor.md) before implementing substantial visual changes.
- For a small refinement to an existing UI, inspect the relevant components, styles, and visual baseline. Preserve the current visual language and product behavior. Use the playbook only when it adds a needed check.
- For a bare `$impeccable` invocation, use the [routing guide](reference/routing.md) with the context it needs. For a workflow question, answer from the guide and relevant playbook.

For work that needs product, design, or platform context, run `<skill-base-dir>/scripts/impeccable context` once from the user's project, with `--target <path>` when a route or source file is known. On Windows, use the matching `impeccable.cmd` launcher when needed. If the launcher is unavailable, read the project's existing PRODUCT.md, DESIGN.md, and relevant surface brief directly. Stay within the host's authorization for tool setup and project edits.

## Verify the result

Check the affected states and viewports together. Fix supported findings in one batch and confirm them with a focused second check when needed. Use the host's browser or native verification route. Inspect stable visual fixtures and component evidence when the app cannot run. Keep project repair, hook management, and command shortcuts scoped to explicit requests.

Run review and specialist steps inline by default. Use subagents only when the user explicitly requests them and the host supports the requested route.
