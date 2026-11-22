---
name: plant-linked-wt
description: Creates a task's linked worktree as `REPO-WT-FEATURE` in the repository's `WS-` workspace folder, on the task's feature branch, creating the branch if missing.
when_to_use: Trigger on starting a task on a feature branch, even when the user does not ask for a worktree; also "new worktree for this feature", "work in a linked worktree", "don't touch main", `git worktree add`. Not for removing a worktree.
metadata:
  version: 1.5.1
---

## Tend Linked Worktree
Give each task, often a plan or suite, one linked worktree on its single [feature branch](#feature-branch), so the main worktree stays untouched.
Never share a linked worktree across tasks or switch its branch, nor split a plan or suite per Movement.
A linked worktree sits inside the repository's workspace folder, named `REPO-WT-FEATURE`:
```text
WS-kaye-library/
├── kaye-library/                         # main worktree, on dev
└── kaye-library-WT-add-search-filter/    # linked worktree, on add-search-filter
```
- `WS-`: prefix of a workspace folder, which holds several worktrees
- `-WT-`: infix marking a linked worktree
### Plant the Linked Worktree
Plant the task's linked worktree as `REPO-WT-FEATURE` in the workspace folder, linked to the task's existing feature branch; if none exists, create the branch with the worktree.