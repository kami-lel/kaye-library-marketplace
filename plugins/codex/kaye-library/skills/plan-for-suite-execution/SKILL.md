---
name: plan-for-suite-execution
description: Executes approved Plan file, 1 Movement per turn — Movement In, work, present with link back, Movement Out. Plan file doubles as saved state, so pause and resume carry across sessions
when_to_use: On Plan file preface; on instruction to begin, continue, pause, or resume; on any *continue* shorthand. Also mid-run on bug, false assumption, wrong Movement, user redirect — halt and rework live here. Not for drafting Plans
metadata:
  version: 1.4.0
---

## Movement and Suite
A **Suite** is a workflow for explicit, multi-round user tasks — not simple, implicit, or single-round work — made up of multiple **Movements**, each one a division of that Suite sized for when the whole cannot be held at once.
- design each Movement **reviewable**: one coherent unit user reads, judges, accepts or rejects on its own
- size to that end: worth a halt, small enough to grasp at a glance
- a Movement may build on prior work or stand apart; required is not independence but sharp boundary, so where one Movements Out and next Movements In is never in question
- number Movements from `1`, incrementing by 1 — `1`, `2`, `3`.
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
### Plan for Suite: Bar 3: Execution
Starts only after the user approves the Plan. Follow Plan order — nothing skipped, nothing combined.
If not already answered, ask whether to run under `cascade-all-movements` or `halt-each-movement`.
Each Movement runs these steps in order:
1. Movement In: enter the Movement the Plan names next, or on resume the one Status names
2. Task: do its work, touching nothing outside the Movement's boundary
3. [Movement Recap](#movement-recap)
4. Movement Out: return control to user
Check the Movement's Party at Movement In. Your own Movements run as above; any other party follows [Movement Parties in Execution](#movement-parties-in-execution).
Movement order binds your judgement, not the user's. Out of sequence, several at once, one skipped, the Plan set aside — obey without protest, noting which Movements are left.
##### Saved State
The Plan file doubles as the run's saved state, so a run survives the end of a session:
- Normal Execution: leave the Plan file untouched, no Status update between Movements
- Pause: only when the user explicitly states "pause", never on a halt; then set each Movement's Status keyword to where the run stands
- Resume: read each Movement's Status, Movement In to the earliest not `Done` or `Dropped`; on a mismatch with the workspace, halt per [Reworking the Plan](#reworking-the-plan)
Status keywords, written only on a pause or a rework. Each Movement carries exactly one keyword at any moment:
- `Pending`: not entered yet, the starting keyword
- `Done`: closed Working
- `Halted`: stopped, awaiting rework
- `Dropped`: removed by rework
##### Movement Parties in Execution
For a user Movement, never do the work yourself. Guide interactively:
1. Movement In: say the Movement is theirs and its goal
2. give one step at a time; wait for their report before the next
3. halt per [Reworking the Plan](#reworking-the-plan) if a report contradicts the Plan
4. settle the End State by their confirmation or your check, and say which
5. Movement Out once it holds
For another party, hand over steps and End State, await its report, then verify.
##### Reworking the Plan
Halt the moment reality stops matching the Plan — a bug, a false assumption, a wrong or unnecessary Movement, unaccounted-for work, a user redirect, anything unanticipated. Never work around it.
1. present the finding: the Plan's assumption, the reality, and the cost to the Movements still ahead
2. rewrite the Plan whole — edit it in place, or author an entirely new file — never a diff, excerpt, or the rework alone. Keep completed Movements untouched and numbered; revise, remove, or add the rest as the finding demands
3. set every Movement's Status keyword per [Bar 2: Write the Plan](#bar-2-write-the-plan), so the file reads cold as exactly how far the run got and what the finding cost
4. never renumber to make room. A split Movement keeps its number and gains sub-Movements beneath it — `Movement 1` becomes `Movement 1.1` and `Movement 1.2`
5. present the revised Plan and hold for approval, as in [Bar 2: Write the Plan](#bar-2-write-the-plan)
6. once approved, Movement In to the earliest unfinished Movement, and not sooner
#### Movement Recap
Always end the Turn with a 2-line [Turn Progress Dispatch](#turn-progress-dispatch), each line prefixed per [Movement Notation](#movement-notation):
```
🎏 🧩3\7 Rewrote the Entry Point
🧭 🧩4\7 Wire Up the Config Loader
```
Except when the entire Plan is completed — then end with a 1-line Turn Progress Dispatch naming the Plan instead:
```
🏁 Auth Refactor
```
#### {[git] Usage}
Each Movement lands as one git commit, performed as the chosen skill directs. A Movement that changes no workspace file, such as a user Movement, commits nothing.