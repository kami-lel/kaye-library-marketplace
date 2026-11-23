---
name: land-feature
description: 'Lands a feature branch on `dev`: runs every Ready for Feature Landing movement, merges the branch into `dev` with a typed Feature Landing message, then runs Scrub After Feature Landing.'
when_to_use: 'Reach for this when a finished feature branch should be merged: "land this feature," "merge this into dev," "finish and merge." Not for prepping docs alone (use the ready-land-feature skill) or releasing a version.'
metadata:
  version: 1.6.0
---

## Movement and Suite
A **Suite** is a workflow for explicit, multi-round user tasks — not simple, implicit, or single-round work — made up of multiple **Movements**, each one a division of that Suite sized for when the whole cannot be held at once.
- design each Movement **reviewable**: one coherent unit user reads, judges, accepts or rejects on its own
- size to that end: worth a halt, small enough to grasp at a glance
- a Movement may build on prior work or stand apart; required is not independence but sharp boundary, so where one Movements Out and next Movements In is never in question
- number Movements from `1`, incrementing by 1 — `1`, `2`, `3`.
These extend the discourse units with the Suite's own terms. Abbreviations are decode-only: always use the full term in your response:
- mvmt:movement (self-contained, reviewable unit of a task; usually Movement=Turn, sometimes spans multiple Rounds)
- 🧩:movement
- suite (unit contains 1+ Movements)
in general: Round < Movement < Suite
Mark a Movement's close, or the whole Suite's, in a [Turn Progress Dispatch](#turn-progress-dispatch) with:
- 🎏:Movement finished (one reviewable chunk of the task closes)
- 🏁:task/Suite completed (nothing pending anywhere; rare, expect several 🚩/🎏 before one)
The example below runs across several Turns of one conversation. A line in parentheses names the situation around the decorative, never text to write in an actual response.
```markdown
(you wire the loader to the new columns, closing Movement 1)
🎏 Config Loader Reading New Columns
(new Turn, you rebuild the entry point on the loader, the last Movement)
🎏 Entry Point Rebuilt on the Loader
🏁 Schema Migration Suite Complete
```
### {[git] Usage}
A single Movement often corresponds to one git commit.
### Movement Notation
```
🧩3\7 Rewrote the Entry Point
🧩5
```
Aggressively use one of these 2 forms for every mention of a Movement in your response: `🧩a\b SUMMARY` or `🧩a`:
- `a` current Movement number
- `b` total Movement count
- `SUMMARY` short description of the Movement, in [Title Case](#letter-case-title-case)
----
Except in a markdown heading: spell out `Movement a` instead, eg `## Movement 5`.
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