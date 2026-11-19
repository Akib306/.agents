# Example staged rollout

For a risky change behind a feature flag, a service might deploy to staging and run its smoke tests, deploy the same artifact to production with the flag off, then enable the flag for staff and a small user cohort. It might increase exposure from 5% to 25%, 50%, and 100% after enough traffic accumulates at each step. Adjust stages and windows to the service's risk, traffic, and incident response coverage.

Use comparable control and canary traffic. Inspect error rate, tail latency, and the primary user outcome. Define an absolute floor for sparse errors or traffic, when ratios would be unstable. Hold when telemetry is missing or crosses a watch threshold. Roll back promptly for confirmed data loss or integrity issues, or when the release crosses the service's rollback threshold.

Confirm recovery after disabling the flag or redeploying the known-good artifact. Document which data and migrations remain active, who monitors the service, and who removes the temporary flag.
