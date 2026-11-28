---
name: tend-linked-wt
description: Places a task's linked worktree, one per task on its branch of any kind, as `REPO-WT-BRANCH` inside the repository's `WS-` workspace folder, and removes it once its edits are merged into the branch it merges back into.
when_to_use: Trigger on starting, continuing, or finishing a task in a linked worktree, on a feature branch, an instrumental branch, or any other, even when the user does not say so; also "new worktree for this feature", "work in a linked worktree", "don't touch main", "remove the worktree", `git worktree add`, `git worktree remove`.
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
### Plant the Linked Worktree
Plant the task's linked worktree as `REPO-WT-BRANCH` in the workspace folder, linked to the task's existing branch. If none exists, create the branch with the worktree, from the branch it will merge back into: the integration branch for a feature branch, the feature branch for an instrumental branch.
### Uproot the Linked Worktree
Once the task is done, uproot its linked worktree, but only after every edit it holds is committed and merged into the branch it merges back into: the main worktree's branch for a feature branch, the feature branch for an instrumental branch. If any edit is not, stop and report.