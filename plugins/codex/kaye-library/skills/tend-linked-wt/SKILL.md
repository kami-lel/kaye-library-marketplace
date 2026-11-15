---
name: tend-linked-wt
description: Places a feature branch's linked worktree, one per task, as `REPO-WT-FEATURE` inside the repository's `WS-` workspace folder, and removes it once its edits reach the main worktree.
when_to_use: Trigger on starting, continuing, or finishing a task on a feature branch in a linked worktree, even when the user does not say so; also "new worktree for this feature", "work in a linked worktree", "don't touch main", "remove the worktree", `git worktree add`, `git worktree remove`.
metadata:
  version: 1.3.2a0
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
### Uproot the Linked Worktree
Once the task is done, uproot its linked worktree, but only after every edit it holds has reached the main worktree, ie committed and merged into the main worktree's branch; if any edit has not, stop and report.