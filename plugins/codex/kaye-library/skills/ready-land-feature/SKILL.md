---
name: ready-land-feature
description: Records a feature branch's changes into `CHANGELOG.md` and updates `AGENTS.md` and `CONTEXT.md` to match, syncing all affected docs in one pass before a merge, then commits the work.
when_to_use: Reach for this when wrapping up or merging a feature branch — "prep for merge," "finish this feature," "document what I changed," "update docs before merging." Not for cutting a versioned release (use the release skill) or general doc edits unrelated to a branch.
metadata:
  version: 1.4.0
---

# Git
## feature branch
A **feature branch** is a branch cut from `dev` to build one feature in isolation, then merged back.
Name it starting with a verb, never with a `feature/` prefix, eg `add-search-filter`, `fix-token-refresh`.
Assume local `HEAD` is the feature branch. Observe it with `git log dev..HEAD`: the commits it holds that `dev` lacks.
### discover feature branch
Learn what the finished [feature branch](#feature-branch) delivers and why:
- read the current conversation for what was built and why
- understand the change set from both sources: `git log dev..HEAD` and the `[Unreleased]` entries of `CHANGELOG.md`; fold them together so nothing is stated twice
- if the two together leave the change unclear, read the change directly: `git diff dev...HEAD`
## Ready for Feature Landing
Before merging the current [feature branch](#feature-branch), sync the docs it affects. Work in Movements; edit affected files in place and leave the rest untouched.
#### Movement 1~3: Sync Unit Test
If the project has unit tests, run [Sync Unit Test](#sync-unit-test) first.
##### {[Claude:Skill] Usage}
Invoke `sync-unit-test` skill via `Skill` tool.
##### {[Hermes:skill_view] Usage}
Load `sync-unit-test` skill with `skill_view`.
#### Movement 4: Learn the Feature Branch
Run [Discover Feature Branch](#discover-feature-branch), then use the change set it yields throughout Movement 5 & 6.
#### Movement 5: Record the Change Set in the CHANGELOG
Run [Maintain CHANGELOG](#maintain-changelog), recording the change set per [Repository CHANGELOG Writer](#repository-changelog-writer). The unreleased-only and deduplication rules come from that skill.
#### Movement 6: Sync AGENTS and CONTEXT
Run [Maintain Repository AGENTS](#maintain-repository-agents), updating any command, convention, or constraint the branch moved, per [Repository AGENTS Writer](#repository-agents-writer). Then update `CONTEXT.md` directly for any architecture the branch moved, per [Repository CONTEXT Writer](#repository-context-writer).
#### Movement 7: Commit the Work
Index the changes this work made, then run [Commit Sense](#commit-sense) to commit them.