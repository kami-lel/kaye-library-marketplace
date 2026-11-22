---
name: release-version
description: 'Releases the project: runs every Ready for Version Release movement, merges the branch into `main` with a typed release message, tags the merge with its `v` version, then runs Scrub After Version Release.'
when_to_use: 'Reach for this when a release should go out: "release 1.2.0," "cut a release and tag it," "merge to main and tag." Not for prepping the release alone (use the ready-release-version skill) or landing a feature branch (use the land-feature skill).'
metadata:
  version: 1.5.1
---

## Perform Version Release
Release the project: ready it, merge it into `main`, then tag the merge, so every tag marks a release with current docs.
#### Movement 1~6: Ready the Release
Run [Ready for Version Release](#ready-for-version-release) whole. Keep the version it settles for Movement 8~11.
#### Movement 7: Commit the Work
Index the changes Movement 1~6 made, then run [Commit Sense](#commit-sense) to commit them.
#### Movement 8: Merge into Main
Merge the current branch per [Commit Sense For Branch Merging](#commit-sense-for-branch-merging) (into main):
1. `git switch main`, then `git merge --no-ff --no-commit SOURCE`: a merge commit records the release, and the pause lets you word it
2. on conflicts, run [Resolve Merge Conflict](#resolve-merge-conflict), then go on
3. write the message, Git's drafted one read from `git rev-parse --git-path MERGE_MSG`, then `git commit` once
#### Movement 9: Tag the Release
Tag the merge commit with `v` plus the version: `git tag vVERSION`, eg `git tag v1.0.0`.
#### Movement 10~11: Scrub After the Release
Run [Scrub After Version Release](#scrub-after-version-release) whole, once the tag lands. If any earlier Movement halts, report where and why in one line, then stop.