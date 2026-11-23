---
name: ready-land-feature
description: Records a feature branch's changes into `CHANGELOG.md` and updates `AGENTS.md` and `CONTEXT.md` to match, syncing all affected docs in one pass before a merge, then commits the work.
when_to_use: Reach for this when wrapping up or merging a feature branch — "prep for merge," "finish this feature," "document what I changed," "update docs before merging." Not for cutting a versioned release (use the release skill) or general doc edits unrelated to a branch.
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
### {[Claude:Skill] Usage}
Invoke `sync-unit-test`, `maintain-changelog`, `maintain-repo-agents`, and `commit-sense` skills via `Skill` tool.