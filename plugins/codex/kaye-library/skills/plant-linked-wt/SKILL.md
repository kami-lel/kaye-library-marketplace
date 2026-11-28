---
name: plant-linked-wt
description: Creates a task's linked worktree as `REPO-WT-BRANCH` in the repository's `WS-` workspace folder, on the task's branch of any kind, creating the branch if missing.
when_to_use: Trigger on starting a task on its own branch, a feature branch or a voice branch alike, even when the user does not ask for a worktree; also "new worktree for this feature", "work in a linked worktree", "don't touch main", `git worktree add`. Not for removing a worktree.
metadata:
  version: 1.6.1
---

## Tend Linked Worktree
Give each task, often a plan or suite, one linked worktree on its single branch, so the main worktree stays untouched. The branch may be of any kind: a [feature branch](#feature-branch), a voice branch, a hotfix or release branch, ~.
Never share a linked worktree across tasks or switch its branch, nor split a plan or suite per Movement. The 1 split allowed: each instrumental Voice of a Suite gets its own linked worktree on its voice branch, whatever its mode.
A linked worktree sits inside the repository's workspace folder, named `REPO-WT-BRANCH`:
```text
WS-kaye-library/
├── kaye-library/                                # main worktree, on dev
├── kaye-library-WT-add-search-filter/           # linked worktree, on add-search-filter
└── kaye-library-WT-add-search-filter-violin/    # linked worktree, on voice branch add-search-filter-violin
```
- `WS-`: prefix of a workspace folder, which holds several worktrees
- `-WT-`: infix marking a linked worktree
### Plant the Linked Worktree
Plant the task's linked worktree as `REPO-WT-BRANCH` in the workspace folder, linked to the task's existing branch. If none exists, create the branch with the worktree, from the branch it will merge back into: the integration branch for a feature branch, the feature branch for a voice branch.