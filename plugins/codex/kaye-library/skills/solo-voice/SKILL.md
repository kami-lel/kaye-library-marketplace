---
name: solo-voice
description: 'Runs 1 instrumental Voice of a Suite whole, agent only, as a subagent or in its own session: its Movements in order on its instrumental branch, 1 commit each, then 1 report to the main session'
when_to_use: When dispatched to run an instrumental Voice (🎻 Violin, 🎺 Trumpet, ~) of a Suite, by a subagent prompt or in a session that names the Plan file and the Voice. Not for the Main Voice (`play-suite`) or drafting Plans (`plan-for-suite`)
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
### Plan for Suite: Execution
Starts only after the user approves the Plan. Follow Plan order — nothing skipped, nothing combined.
The Plan file holds the context and Terrain: start from it, read your Movements there, and explore the repository only when a Movement needs more. Leave the Plan file untouched unless a rule says to write it.
Never work around a mismatch with the Plan, an End State that will not hold, or anything a Movement cannot settle alone.
Each Voice works only on its own branch and in its own worktree, and never touches another Voice's.
Housekeeping splits by Voice: the instrumental Voice cuts its instrumental branch and plants its linked worktree, as its own opening Movement; the Main Voice merges, uproots, and prunes, as its own closing Movement. Any other housekeeping Movement is an ordinary Movement.
Each Movement runs these steps in order:
1. Movement In: enter the Movement next in order
2. Task: do its work, touching nothing outside the Movement's boundary, until its End State holds
#### {[git] Usage}
1 Movement = 1 commit. A Movement that edits no workspace file, such as a user Movement, commits nothing.
### Solo Voice
You run 1 instrumental Voice of a Suite whole. The main session names the Plan file and the Voice, and nothing else.
- run the Voice's Movements per [Plan for Suite: Execution](#plan-for-suite-execution), its opening Movement first
- work only in the Voice's linked worktree, on its instrumental branch
- never merge or prune the instrumental branch: the main session merges the Voice back
- never ask the user anything, nor wait for an approval
- on a mismatch with the Plan, an End State that will not hold, or anything a Movement cannot settle alone, stop and report
End with 1 report, nothing after it: per Movement, its short commit hash and its End State (met, or why not), then where you stopped and what remains unrun.
#### {[Claude:Agent~] Lack}
End your final reply with the report, for the user to carry back to the main session.