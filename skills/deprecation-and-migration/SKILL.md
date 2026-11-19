---
name: deprecation-and-migration
description: Plan a live API, service, or schema migration with dependent consumers, compatibility windows, or production data.
---

# Deprecation and Migration

1. Identify consumers, contracts, stored data, owners, and real usage. Establish whether consumers need a replacement, adapter, migration tooling, or time to update.
2. Choose a compatibility window and migration path. Provide an actionable notice with affected interfaces, the replacement or retirement date, and a way to verify migration. Track remaining usage and help consumers move with as little manual work as possible.
3. For a live schema change, use expand and contract. Add the new shape without breaking existing readers or writers. Synchronize mixed-version writes and backfill in bounded, restartable batches. Verify parity, switch reads, observe the new path, then remove the old shape only after old consumers have drained.
4. Verify recovery at each stage. Use a tested rollback when it preserves data. When reversal would lose new writes or repeat irreversible work, use an appropriate recovery plan such as forward repair, restore or replay, with a verified recovery point. Check lock behavior, concurrent writes, and deployment ordering for the actual database.
5. Remove old code, data, flags, and documentation after dependency and usage evidence shows the removal is safe. Verify the migrated path and report remaining consumers or rollout obligations.
