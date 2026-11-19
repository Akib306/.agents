---
name: shipping-and-launch
description: Prepare or verify a production release, canary, or rollback using service-specific checks and rollout criteria.
---

# Shipping and Launch

1. Identify the release artifact, affected environments and users, and the deployment authorization. Check applicable CI status, compatibility risks, migrations, and the critical user paths.
2. Define who can pause or roll back, how to do it, and how to verify recovery. Confirm the previous artifact or disable flag is available. For data changes, check recovery and compatibility separately from application rollback.
3. Verify that the metrics and alerts needed for the decision are observable. Set advance, hold, and rollback criteria from service SLOs, error budget, baseline, and business or data-integrity signals. Choose a rollout sequence and observation windows appropriate to the risk.
4. Check the deployed artifact, health, critical smoke tests, and recent metrics at each stage. Hold on ambiguous results and roll back under the agreed criteria. Record the evidence and decision.
5. Confirm the final rollout state and responsibility for follow-up, including temporary flags and alerting.

Read the [rollout example](references/rollout-example.md) when choosing stages and signals for a release.
