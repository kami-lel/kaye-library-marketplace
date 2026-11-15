---
name: land-feature
description: 'Lands a feature branch on `dev`: runs every Ready for Feature Landing movement, then merges the branch into `dev` with a typed Feature Landing message.'
when_to_use: 'Reach for this when a finished feature branch should be merged: "land this feature," "merge this into dev," "finish and merge." Not for prepping docs alone (use the ready-land-feature skill) or releasing a version.'
metadata:
  version: 1.4.0
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
#### Movement 9: Report and Ask Approval
Reply as below, asking up to 3 approvals: push `dev`; delete the feature branch (merged, so safe to drop); uproot its linked worktree, asked only when you work in a linked worktree. If any Movement halts, report where and why in one line, then stop.
<post-landing-output-example>
🚩🐙 Feature Landed: add status filter to Search page
✍️ ⓑ push `dev` to origin?
✍️ ⓒ delete feature branch `add-search-filter`?
✍️ ⓓ uproot linked worktree `kaye-library-WT-add-search-filter`?
ⓐ all of above
</post-landing-output-example>
#### Movement 10: Push and Delete
Run only the approved actions, in order ⓑ, ⓓ, ⓒ, since Git refuses to delete a branch while a worktree holds it; ⓐ approves all three:
- ⓑ `git push origin dev`
- ⓒ `git branch -d FEATURE`, never `-D`
- ⓓ invoke `uproot-linked-wt`
Reply once, after all are done:
<post-push-delete-output-example>
🚩🐙 pushed `dev` to origin
🚩🐙 uprooted `kaye-library-WT-add-search-filter`
🚩🐙 deleted `add-search-filter`
</post-push-delete-output-example>