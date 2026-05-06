---
name: using-git-worktrees-optimized
description: Use when parallel work, risky experiments, or isolated branch tasks would benefit from separate working directories.
---

# Git Worktrees Optimized

Use worktrees to isolate branch state without cloning again.

## Flow

1. Check current branch and uncommitted changes.
2. Create a named worktree for the target branch.
3. Keep dependencies, ports, and generated files isolated.
4. Commit or clean each worktree independently.
5. Remove worktrees only after confirming paths and branch state.

## Gotchas

- Do not delete a worktree path without verifying it.
- Do not share build artifacts across incompatible branches.
- Do not forget which terminal is in which worktree.
