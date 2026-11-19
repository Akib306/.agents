---
name: performance-optimization
description: Profile a measured application slowdown or performance regression, or implement against a stated performance target.
---

# Performance Optimization

1. Choose the user-visible or operational metric and a representative workload. Record the baseline, command, data, configuration, and cache state. Repeat noisy measurements.
2. Follow the evidence to the bottleneck. Use the relevant trace, query plan, heap profile, or timing. Measure expensive paths before introducing caching, indexing, or rendering changes.
3. Change one cause at a time when attribution matters. Preserve correctness, including tenant and permission boundaries in caches, stable pagination, and the write costs of new indexes.
4. Re-measure with the same conditions. Compare the effect with run-to-run variance and run the relevant correctness checks. Keep an optimization when the observed improvement justifies the complexity. Record useful failed experiments where future work can find them.
5. Use the project's performance targets. Add a regression check or field measurement when the benefit warrants ongoing monitoring.

Use [optimization patterns](references/optimization-patterns.md) for database and caching recipes, frontend bottlenecks, and example web budgets.
