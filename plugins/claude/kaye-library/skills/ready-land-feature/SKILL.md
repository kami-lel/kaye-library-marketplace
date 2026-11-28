---
name: ready-land-feature
description: Records a feature branch's changes into `CHANGELOG.md` and updates `AGENTS.md` and `CONTEXT.md` to match, syncing all affected docs in one pass before a merge, then commits the work.
when_to_use: Reach for this when wrapping up or merging a feature branch — "prep for merge," "finish this feature," "document what I changed," "update docs before merging." Not for cutting a versioned release (use the release skill) or general doc edits unrelated to a branch.
metadata:
  version: 1.6.2
---

## Movement, Voice, and Suite
An explicit, multi-round user task runs as 3 nested units: Suite, Voice, and Movement. Never use them for simple, implicit, or single-round work.
**Suite**: the whole workflow for 1 such task
- holds 1+ Voices, the Main Voice always among them
- works on its feature branch, often 1 Suite = 1 feature branch, which every instrumental branch merges back into
- completes once every Voice has merged back and no Movement remains
**Voice**: 1 line of Movements within a Suite, run in order
- the **Main Voice** is the Suite's own line, marked 🧩: every Movement outside the other Voices, user Movements included; only the main session runs it
- every other Voice is an **instrumental Voice**, marked by its instrument emoji: agent only, with no user Movement, approval, or question inside it
- every Voice must be able to run in parallel with the rest, never waiting on another Voice's unmerged work
- each instrumental Voice works on its own instrumental branch and linked worktree, cut from the feature branch and merged back into it once its Movements are done
**Movement**: 1 division of a Voice, sized for when the whole cannot be held at once
- design each Movement **reviewable**: one coherent unit user reads, judges, accepts or rejects on its own
- size to that end: worth a halt, small enough to grasp at a glance
- a Movement may build on prior work or stand apart; required is not independence but sharp boundary, so where one Movements Out and next Movements In is never in question
- number each Voice's Movements from `1`, incrementing by 1 — `1`, `2`, `3`.
Name each instrumental Voice after an instrument, and mark it with that instrument's emoji, taken in this order:
- 🎻:violin
- 🎺:trumpet
- 🎷:saxophone
- 🎸:guitar
- 🪕:banjo
- 🪈:flute
- 🎹:piano
- 🪗:accordion
These extend the discourse units with the Suite's own terms. Abbreviations are decode-only: always use the full term in your response:
- mvmt:movement (self-contained, reviewable unit of a task; usually Movement=Turn, sometimes spans multiple Rounds)
- 🧩:movement
- voice (line of Movements within a Suite; any but the Main Voice is an instrumental Voice: agent only, soloed by a subagent or run in its own session, in parallel on its instrumental branch, then merged back into the feature branch)
- suite (unit contains 1+ Voices)
in general: Round < Movement < Voice < Suite
### {[git] Usage}
Commit each Movement's edits as exactly one git commit: 1 Movement = 1 commit.
Often 1 Suite = 1 feature branch. 1 Voice = 1 instrumental branch, cut from the feature branch and merged back into it.
### {[Claude:TodoWrite] Usage}
One `TodoWrite` entry per Movement in the Suite, every Voice included — 1:1, never merged or split. List the Main Voice's entries first, then each instrumental Voice's in instrument order, each Voice's in Movement order.
- `content`: prefix + Movement imperative
- `activeForm`: prefix + present continuous
Status flow: `pending` at Seed (before Movement 1 opens) → `in_progress` on Open → `completed` on Close, once Working state is verified.
Rules:
- exactly 1 entry `in_progress` in the Main Voice, plus 1 per open instrumental Voice
- Movement added or dropped mid-Suite: edit the array in the call that closes the current Movement
### Dispatch Marks
Mark a Movement's close, an instrumental Voice's merge back, or the whole Suite's close in a [Turn Progress Dispatch](#turn-progress-dispatch) with:
- 🎏:Movement finished (one reviewable chunk of the task closes)
- 🎌:Voice finished (instrumental Voice merges back into the feature branch)
- 🏁:task/Suite completed (nothing pending anywhere; rare, expect several 🚩/🎏 before one)
On a 🎏 line closing a Main Voice Movement, and only there, write the Movement prefix as `🧩a\b`, `b` the Main Voice's total Movement count. Every other line, 🧭 included, keeps its usual Movement prefix, with no total.
Only the main session writes these marks. An instrumental Voice, in either mode, writes none of them, neither 🎏 nor a `\b` total; the main session marks it once, with 🎌, at its merge back.
The example below runs across several Turns of one conversation. A line in parentheses names the situation around the decorative, never text to write in an actual response.
```markdown
(you wire the loader to the new columns, closing Movement 1 of 2)
🎏 🧩1\2 Config Loader Reading New Columns
🧭 🧩2 Rebuild the Entry Point
(the Violin Voice reports its fixtures rewritten, and you merge it back)
🎌 Violin Test Fixtures Merged Back
(new Turn, you rebuild the entry point on the loader, the last Movement)
🎏 🧩2\2 Entry Point Rebuilt on the Loader
🏁 Schema Migration Suite Complete
```
### Movement Notation
```
🧩3 Rewrote the Entry Point
🧩5
🎻2 Added Parser Tests
```
Aggressively use one of these 2 forms for every mention of a Movement in your response: `🧩a SUMMARY` or `🧩a`:
- `a` Movement number, counted within its own Voice
- `SUMMARY` short description of the Movement, in [Title Case](#letter-case-title-case)
- in a Voice other than the Main Voice, put that Voice's instrument emoji in place of 🧩, eg `🎻2`
Write no total Movement count unless a rule names one.
----
Except in a markdown heading: spell out `Movement a` instead, eg `## Movement 5`.
#### {[Claude:TodoWrite] Usage}
`TodoWrite` Examples, with prefix `🧩a SUMMARY` or `🎻a SUMMARY`
Seed:
```json
{
  "todos": [
    {
      "content": "🧩1 Rewrite the Entry Point",
      "status": "pending",
      "activeForm": "🧩1 Rewriting the Entry Point"
    },
    {
      "content": "🧩2 Move the Parser to Its Own Module",
      "status": "pending",
      "activeForm": "🧩2 Moving the Parser to Its Own Module"
    },
    {
      "content": "🧩3 Wire the Parser Into the Entry Point",
      "status": "pending",
      "activeForm": "🧩3 Wiring the Parser Into the Entry Point"
    },
    {
      "content": "🎻1 Update the Test Fixtures",
      "status": "pending",
      "activeForm": "🎻1 Updating the Test Fixtures"
    },
    {
      "content": "🎻2 Add Parser Tests",
      "status": "pending",
      "activeForm": "🎻2 Adding Parser Tests"
    }
  ]
}
```
Open Movement 2 while the Violin Voice runs — resend whole array, 2 statuses change:
```json
{
  "todos": [
    {
      "content": "🧩1 Rewrite the Entry Point",
      "status": "completed",
      "activeForm": "🧩1 Rewriting the Entry Point"
    },
    {
      "content": "🧩2 🥁 Move the Parser to Its Own Module",
      "status": "in_progress",
      "activeForm": "🧩2 🥁 Moving the Parser to Its Own Module"
    },
    {
      "content": "🧩3 Wire the Parser Into the Entry Point",
      "status": "pending",
      "activeForm": "🧩3 Wiring the Parser Into the Entry Point"
    },
    {
      "content": "🎻1 Update the Test Fixtures",
      "status": "in_progress",
      "activeForm": "🎻1 Updating the Test Fixtures"
    },
    {
      "content": "🎻2 Add Parser Tests",
      "status": "pending",
      "activeForm": "🎻2 Adding Parser Tests"
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
Run [Maintain Repository AGENTS](#maintain-repository-agents), updating any command, convention, or constraint the branch moved in the layer nearest the changed files, per [Repository AGENTS Writer](#repository-agents-writer). Then update the `CONTEXT.md` nearest the changed files directly for any architecture the branch moved, per [Repository CONTEXT Writer](#repository-context-writer).
#### Movement 7: Commit the Work
Index the changes this work made, then run [Commit Sense](#commit-sense) to commit them.
### {[Claude:Skill] Usage}
Invoke `sync-unit-test`, `maintain-changelog`, `maintain-repo-agents`, and `commit-sense` skills via `Skill` tool.