---
name: land-feature
description: 'Lands a feature branch on `dev`: runs every Ready for Feature Landing movement, merges the branch into `dev` with a typed Feature Landing message, then runs Scrub After Feature Landing.'
when_to_use: 'Reach for this when a finished feature branch should be merged: "land this feature," "merge this into dev," "finish and merge." Not for prepping docs alone (use the ready-land-feature skill) or releasing a version.'
metadata:
  version: 1.5.0
---

## Perform Feature Landing
Land the current [feature branch](#feature-branch) on `dev`: ready it, then merge it, so `dev` never receives stale docs.
#### Movement 1~7: Ready the Feature Branch
Run [Ready for Feature Landing](#ready-for-feature-landing) whole. Continue only once its commit lands; keep its [feature branch summary](#feature-branch-summary) for Movement 8.
#### Movement 8: Merge into Dev
Merge per [Commit Sense For Branch Merging](#commit-sense-for-branch-merging) (feature into dev). When you work in a linked worktree, do every step in the main worktree, since it holds `dev`.
1. `git switch dev`, then `git merge --no-ff --no-commit FEATURE`: a merge commit records the landing, and the pause lets you word it
2. on conflicts, run [Resolve Merge Conflict](#resolve-merge-conflict), then go on
3. write the message, Git's drafted one read from `git rev-parse --git-path MERGE_MSG`, then `git commit` once
Stop at the merge commit: push and branch deletion wait for the approval of Movement 9.
#### Movement 9~10: Scrub After the Landing
Run [Scrub After Feature Landing](#scrub-after-feature-landing) whole, once the merge commit lands. If any earlier Movement halts, report where and why in one line, then stop.
### {[Claude:Skill] Usage}
Invoke `ready-land-feature`, `commit-sense-branch-merging`, `resolve-merge-conflict`, and `scrub-landed-feature` skills via `Skill` tool.