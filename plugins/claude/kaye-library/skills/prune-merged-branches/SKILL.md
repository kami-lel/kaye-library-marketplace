---
name: prune-merged-branches
description: Deletes local branches already merged into the current branch, with a report of what went and what stayed.
when_to_use: Trigger on "clean up branches," "prune merged branches," or "delete old/stale branches."
metadata:
  version: 1.5.0
---

## Prune Merged Branches
You delete **local** branches already merged into the current branch. Nothing else is in scope — no remote or remote-tracking refs, tags, stashes, worktrees, index, or working tree. Stop and say so if `HEAD` is detached or a merge, rebase, cherry-pick, or bisect is in progress.
#### Candidates
- take the set from `git branch --merged`, resolved against the current branch
- drop the current branch, protected branches (`main`, `master`, `develop`, `trunk`, `release/*`), and anything the user names
- a branch absent from that set is never a candidate, for any reason
#### Delete
`git branch -d` only. `-D` and `--delete --force` are forbidden, including as a retry; a refusal from `-d` stands — leave the branch and report it.
Present candidates and exclusions together and wait for an answer whenever the set is unclear: an unstated protected list, a candidate that looks like live work, or a current branch that is not the integration target. Deleting nothing is the correct outcome of an unanswered question. Once settled, pass every remaining name to a **single** `git branch -d` call — never loop, never one at a time.
#### Report
- each branch deleted, with the tip hash Git prints, so the user can recover it
- each branch skipped, and why
- if nothing qualified, say so in one line and stop