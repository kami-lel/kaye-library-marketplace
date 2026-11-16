---
name: release-version
description: 'Releases the project: runs every Ready for Version Release movement, merges the branch into `main` with a typed release message, and tags the merge with its `v` version.'
when_to_use: 'Reach for this when a release should go out: "release 1.2.0," "cut a release and tag it," "merge to main and tag." Not for prepping the release alone (use the ready-release-version skill) or landing a feature branch (use the land-feature skill).'
metadata:
  version: 1.4.1
---

## Perform Version Release
Release the project: ready it, merge it into `main`, then tag the merge, so every tag marks a release with current docs.
#### Movement 1~7: Ready the Release
Run [Ready for Version Release](#ready-for-version-release) whole. Keep the version it settles for Movement 9~12.
#### Movement 8: Commit the Work
Index the changes Movement 1~7 made, then run [Commit Sense](#commit-sense) to commit them.
#### Movement 9: Merge into Main
Merge the current branch per [Commit Sense For Branch Merging](#commit-sense-for-branch-merging) (into main):
1. `git switch main`, then `git merge --no-ff --no-commit SOURCE`: a merge commit records the release, and the pause lets you word it
2. on conflicts, run [Resolve Merge Conflict](#resolve-merge-conflict), then go on
3. write the message, Git's drafted one read from `git rev-parse --git-path MERGE_MSG`, then `git commit` once
#### Movement 10: Tag the Release
Tag the merge commit with `v` plus the version: `git tag vVERSION`, eg `git tag v1.0.0`.
#### Movement 11: Report and Ask Approval
Reply as below, asking 3 approvals: push `main` and the tag, prune merged branches, naming each branch to prune (the candidates of [Prune Merged Branches](#prune-merged-branches)), and fast-forward `dev` to `main`, local and remote. If any Movement halts, report where and why in one line, then stop.
<post-release-output-example>
🚩🐙 Minor Release 1.1.0
✍️ ⓑ push `main` and `v1.1.0` to origin?
✍️ ⓒ prune merged branches `add-search-filter`, `fix-login-redirect`?
✍️ ⓓ fast-forward `dev` to `main`, local and origin?
ⓐ all of above
</post-release-output-example>
#### Movement 12: Push, Prune, and Sync Dev
Run only the approved actions, in order; ⓐ approves all three:
- ⓑ `git push origin main vVERSION`
- ⓒ invoke `prune-merged-branches`
- ⓓ fast-forward `dev` to `main`, local and origin; if it cannot fast-forward, report in one line and stop
Reply once, after all are done:
<post-push-prune-output-example>
🚩🐙 pushed `main` and `v1.1.0` to origin
🚩🐙 pruned `add-search-filter`, `fix-login-redirect`
🚩🐙 fast-forwarded `dev` to `main`, local and origin
</post-push-prune-output-example>
### {[Claude:Skill] Usage}
Invoke `ready-release-version`, `commit-sense`, `commit-sense-branch-merging`, `resolve-merge-conflict`, and `prune-merged-branches` skills via `Skill` tool.