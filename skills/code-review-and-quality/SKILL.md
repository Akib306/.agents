---
name: code-review-and-quality
description: Review a requested diff or pull request, or verify a consequential change for bugs, regressions, design risks, and missing checks.
---

# Code Review and Quality

1. Read the task or spec, applicable repository rules, and actual diff. Determine the intended behavior, who relies on it, and what changed across the normal entry points.
2. Follow changed behavior through callers, contracts, and tests. Check edge cases, errors, retries, concurrent updates, and compatibility with older data where relevant. Confirm the verification covers the behavior at risk. Use read-only inspection for review and run focused checks when they add evidence. Use isolated mutation experiments only when specifically needed and authorized.
3. Look for structural changes that make future work harder. Check feature logic in shared modules, duplicate implementations, unclear type boundaries, silent fallbacks, and refactors that relocate complexity. Propose a concrete simpler structure. Keep readability refactors scoped and preserve inputs, outputs, ordering, side effects, and errors.
4. Investigate security, performance, or dependencies when the diff changes those risks. For dependency updates, check the lockfile, upstream changes, relevant advisories, and the affected install or runtime path. Review the project's existing safeguards before proposing new ones.
5. Lead with actionable findings in severity order. For each finding, cite the location, explain how the issue occurs, and describe the impact. Separate required fixes from optional suggestions. If no findings remain, state what was checked and what could not be verified.
