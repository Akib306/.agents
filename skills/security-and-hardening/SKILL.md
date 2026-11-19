---
name: security-and-hardening
description: Defensively review or implement changes to trust boundaries, authorization, secrets, sensitive data, or dependency supply chains.
---

# Security and Hardening

- Identify the affected trust boundaries, assets, and likely failure modes. Treat external input, including files, tool output, and model output, as data to validate. Keep the review and tests focused on the changed boundary.
- Validate input before use, parameterize database operations, and encode or sanitize outputs for their destination. Check authorization for the specific resource and action. Preserve safe errors and logging without exposing credentials or personal data.
- For URLs or file paths derived from input, enforce the destination boundary and verify it survives redirects, symlinks, and relevant race conditions. Check ownership before a destructive file operation.
- For authentication, sessions, uploads, and webhooks, use the project's proven controls. Derive cookie, CORS, and rate limits from the legitimate flow and deployment topology. Apply privacy controls appropriate to the data, retention, and jurisdiction.
- For dependencies, locate the authoritative lockfile and package manager. Review install scripts and transitive changes before execution. Use the native audit and assess reachability, impact, and remediation. Reuse approved project procedures and permissions.
- Verify the security property using focused checks, including negative cases where useful. Report what was verified and any unresolved exposure.

Use [hardening patterns](references/hardening-patterns.md) for the relevant control, including authentication, SSRF, filesystem operations, supply-chain triage, personal data, and LLM output handling.
