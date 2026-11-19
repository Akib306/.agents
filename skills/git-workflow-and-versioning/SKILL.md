---
name: git-workflow-and-versioning
description: Handle requested commits, commit splitting, branches, worktrees, conflicts, or release versioning, tags, and changelogs.
---

# Git Workflow and Versioning

- Start with `git status --short` and inspect the relevant unstaged and staged diffs. Identify existing user changes before staging or resolving conflicts. Follow the repository's branching, commit, review, and release conventions.
- For a requested commit, stage only the intended paths or hunks. Review the staged diff for scope, generated files, and secrets. Run the project's relevant checks and write a message that explains the intent. Split independent changes when requested or when it makes the history easier to review and each commit can stand on its own.
- Before resolving a conflict, identify the operation in progress and understand both sides. Validate the merged behavior and inspect the resulting diff before continuing. Preserve unrelated working-tree changes. If recovery requires discarding changes or rewriting shared history, obtain explicit authorization for the specific operation.
- Use the host's worktree or branch workflow for authorized parallel edits. Check the base and ownership of the worktree before editing or cleaning it up.
- For releases, inspect the project's version source and tag history. For projects using SemVer, use major for breaking changes, minor for backward-compatible features, and patch for backward-compatible fixes. Consider observable behavior and migration needs. Write changelog entries around user impact and verify the tag, release artifact, and changelog refer to the same revision.
- Keep remote operations in the approved scope. Reuse the existing authenticated provider or SSH connection when feasible, batch related operations, and surface unavoidable extra authentication before starting.
