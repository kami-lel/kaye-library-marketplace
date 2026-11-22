---
name: uproot-linked-wt
description: Removes a finished task's linked worktree once every edit in it is committed and merged into the main worktree's branch.
when_to_use: Trigger on finishing a task in a linked worktree or merging its branch, even when the user does not ask; also "remove the worktree", "clean up the worktree", `git worktree remove`. Not for deleting merged branches.
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
### Uproot the Linked Worktree
Once the task is done, uproot its linked worktree, but only after every edit it holds has reached the main worktree, ie committed and merged into the main worktree's branch; if any edit has not, stop and report.