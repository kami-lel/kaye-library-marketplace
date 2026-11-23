---
name: release-version
description: 'Releases the project: runs every Ready for Version Release movement, merges the branch into `main` with a typed release message, tags the merge with its `v` version, then runs Scrub After Version Release.'
when_to_use: 'Reach for this when a release should go out: "release 1.2.0," "cut a release and tag it," "merge to main and tag." Not for prepping the release alone (use the ready-release-version skill) or landing a feature branch (use the land-feature skill).'
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
### {[Claude:TodoWrite] Usage}
One `TodoWrite` entry per Movement in the Suite — 1:1, never merged or split. Entry index gives Movement number `a`; array length gives total `b`.
- `content`: prefix + Movement imperative
- `activeForm`: prefix + present continuous
Status flow: `pending` at Seed (before Movement 1 opens) → `in_progress` on Open → `completed` on Close, once Working state is verified.
Rules:
- exactly 1 entry `in_progress` at a time
- Movement added or dropped mid-Suite: edit the array in the call that closes the current Movement, and rewrite every prefix to the new `b`
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
#### {[Claude:TodoWrite] Usage}
`TodoWrite` Examples, with prefix `🧩a\b SUMMARY`
Seed:
```json
{
  "todos": [
    {
      "content": "🧩1\\3 Rewrite the Entry Point",
      "status": "pending",
      "activeForm": "🧩1\\3 Rewriting the Entry Point"
    },
    {
      "content": "🧩2\\3 Move the Parser to Its Own Module",
      "status": "pending",
      "activeForm": "🧩2\\3 Moving the Parser to Its Own Module"
    },
    {
      "content": "🧩3\\3 Update the Test Fixtures",
      "status": "pending",
      "activeForm": "🧩3\\3 Updating the Test Fixtures"
    }
  ]
}
```
Open Movement 2 — resend whole array, 1 status changes:
```json
{
  "todos": [
    {
      "content": "🧩1\\3 Rewrite the Entry Point",
      "status": "completed",
      "activeForm": "🧩1\\3 Rewriting the Entry Point"
    },
    {
      "content": "🧩2\\3 🥁 Move the Parser to Its Own Module",
      "status": "in_progress",
      "activeForm": "🧩2\\3 🥁 Moving the Parser to Its Own Module"
    },
    {
      "content": "🧩3\\3 Update the Test Fixtures",
      "status": "pending",
      "activeForm": "🧩3\\3 Updating the Test Fixtures"
    }
  ]
}
```
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
### {[Claude:Skill] Usage}
Invoke `ready-release-version`, `commit-sense`, `commit-sense-branch-merging`, `resolve-merge-conflict`, and `scrub-released-version` skills via `Skill` tool.