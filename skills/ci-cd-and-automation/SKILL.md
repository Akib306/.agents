---
name: ci-cd-and-automation
description: Configure or repair CI/CD pipelines, build and test jobs, quality gates, or deployment automation.
---

# CI/CD and Automation

1. Inspect existing workflows, project commands, runner requirements, and the triggering event. Use the project's package manager and lockfile. Reuse its commands and required checks.
2. For a failure, start with the failing job and exact command. Reproduce locally when feasible, then verify the correction in the relevant runner or CI job. Keep new outputs focused on useful failure evidence.
3. For pipeline changes, add or adjust only the checks and jobs warranted by the change. Keep job permissions narrow, separate test credentials from deployment credentials, and restrict secrets and deploy actions to trusted events. Verify skipped jobs and path filters behave correctly for required checks.
4. For deployment automation, verify the intended trigger, environment, artifact identity, and rollback mechanism. Follow the repository's existing review, promotion, and deployment controls.
5. Measure slow jobs before changing them. Cache appropriate dependencies, parallelize independent checks, or select affected tests after confirming the required coverage is preserved.

Open [GitHub Actions examples](references/github-actions.md) for Node jobs, database services, browser tests, preview deploys, or rollback workflows. Treat examples as starting points for the project's actual runner and release process.
