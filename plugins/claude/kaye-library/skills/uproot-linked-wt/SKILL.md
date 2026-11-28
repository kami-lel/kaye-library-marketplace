---
name: uproot-linked-wt
description: Removes a finished task's linked worktree once every edit in it is committed and merged into the branch it merges back into.
when_to_use: Trigger on finishing a task in a linked worktree or merging its branch, even when the user does not ask; also "remove the worktree", "clean up the worktree", `git worktree remove`. Not for deleting merged branches.
metadata:
  version: 1.6.2
---

## Tend Linked Worktree
Give each task, often a plan or suite, one linked worktree on its single branch, so the main worktree stays untouched. The branch may be of any kind: a [feature branch](#feature-branch), an instrumental branch, a hotfix or release branch, ~.
Never share a linked worktree across tasks or switch its branch, nor split a plan or suite per Movement. The 1 split allowed: each instrumental Voice of a Suite gets its own linked worktree on its instrumental branch, whatever its mode.
A linked worktree sits inside the repository's workspace folder, named `REPO-WT-BRANCH`:
```text
WS-kaye-library/
├── kaye-library/                                # main worktree, on dev
├── kaye-library-WT-add-search-filter/           # linked worktree, on add-search-filter
└── kaye-library-WT-add-search-filter-violin/    # linked worktree, on instrumental branch add-search-filter-violin
```
- `WS-`: prefix of a workspace folder, which holds several worktrees
- `-WT-`: infix marking a linked worktree
### Uproot the Linked Worktree
Once the task is done, uproot its linked worktree, but only after every edit it holds is committed and merged into the branch it merges back into: the main worktree's branch for a feature branch, the feature branch for an instrumental branch. If any edit is not, stop and report.