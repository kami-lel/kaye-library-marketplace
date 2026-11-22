---
name: plan-for-suite
description: Splits oversized task into ordered, numbered Movements, then runs them under review — survey repository, write Plan file, hold for approval, execute 1 Movement per turn
when_to_use: 'On large, multi-file, multi-concern work wanted reviewable, not 1 pass. Triggers: plan this, break into Movements, go step by step. Start before any edit, so survey precedes Plan, Plan precedes 1st change. Not for 1-turn tasks'
metadata:
  version: 1.5.1
---

## Movement and Suite
A **Suite** is a workflow for explicit, multi-round user tasks — not simple, implicit, or single-round work — made up of multiple **Movements**, each one a division of that Suite sized for when the whole cannot be held at once.
- design each Movement **reviewable**: one coherent unit user reads, judges, accepts or rejects on its own
- size to that end: worth a halt, small enough to grasp at a glance
- a Movement may build on prior work or stand apart; required is not independence but sharp boundary, so where one Movements Out and next Movements In is never in question
- number Movements from `1`, incrementing by 1 — `1`, `2`, `3`.
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
## Plan for Suite
This uses the [Movement and Suite](#movement-and-suite) concepts on a Plan file — a Plan is a Suite, so it holds multiple Movements.
Three *Bars*:
### Bar 1: Gather
Do **not** start editing. Read before you plan.
Resolve the task's scope from the repository itself — entry points, existing conventions, the files the task will touch, and anything the description leaves ambiguous. Prefer reading the actual code over assuming its shape.
Establish where the project stands **now**: what already exists, what is partially done, what is missing. The Plan starts from the real state, never from a clean slate.
Where the reading leaves intent unclear — scope, priorities, trade-offs, which of several readings is meant — ask the user rather than deciding yourself.
### Bar 2: Write the Plan
The Plan divides the task into Movements.
The Plan must be **readable at a glance** and **workable in order**. Any layout serving both is fine. Record for each Movement:
- Scope: the files it touches, all named, and few
- Statement: what changes and why, in a line or two — never a code dump
- **End State**: what *Working* means once the Movement closes, so review can stop there
- Order: what it depends on, which may only be Movements already done
- Party (who performs it): you, the user, or another party by name; give the user what lies beyond your reach, eg a GUI step, a login, a device, an approval
- Status: always write `Pending` when first writing the Plan
The Plan is a **deliverable** and lives in a **Plan file**, so later Movements can revise it in place. Open the file with the preface below, *verbatim* and ahead of all Plan content, so whoever executes it reads the terms before the first Movement.
<plan-for-suite-preface>
Before working from this file, invoke `execute-plan-for-suite` skill through the `Skill` tool.

Ask whether to run under `cascade-all-movements` or `halt-each-movement`, and follow the chosen skill for how the Movements proceed.
</plan-for-suite-preface>
Hand the Plan to the user and **stop**. The codebase stays exactly as it is until they approve.
##### Plan File
- Name: [Kebab Case](#letter-case-kebab-case) slug of the task, ending `-suite-plan.md`, eg `auth-refactor-suite-plan.md`
- Location: first available of workspace root, repository root, your own temporary location
##### Movement Heading
In the Plan file, head each Movement as an `h3`, `### 🧩a\b: Title`, plus, between number and colon, in order and only when they apply:
- `{party}`: for a Movement that is not yours, never for your own
- `[workspace]`: when the task spans several workspaces or repositories
The user is a party too, by their own name, eg `{John}`.
```
### 🧩5\8 [api]: Wire Up the Config Loader
### 🧩6\8 {John} [api]: Approve the Staging Deploy
```
### {[Claude:Skill] Usage}
Invoke the skill chosen for this run — `cascade-all-movements` or `halt-each-movement` — via `Skill` tool.
Invoke `tend-linked-wt` skill via `Skill` tool for each parallel Movement's linked worktree.
### {[Claude:Enter/ExitPlanMode] Usage}
in Bar 1:
- opens with `EnterPlanMode` tool, so all discovery runs before any edit is possible
in Bar 2:
- delivers the finished Plan through `ExitPlanMode` tool, which is where the user approves it
### {[Claude:AskUserQuestion] Usage}
in Bar 1:
- use `AskUserQuestion` tool to ask user
### {[git] Usage}
Never index or commit the [Plan File](#plan-file), unless the user explicitly asks: it is run scratch, not project history.
----
Parallel execution is an option, never a requirement: independent Movements may run at once, each in its own linked worktree and feature branch per `tend-linked-wt`.
- where a large task splits cleanly, favor disjoint Scopes and few dependencies
- mark each parallel Movement with its peers and its branch
- stay sequential when splitting costs more than it saves, eg shared files, tight coupling
- a Movement depending on parallel ones waits until all their branches merge back
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
- Resume: read each Movement's Status, Movement In to the earliest not `Done` or `Dropped`; on a mismatch with the workspace, halt per [Plan for Suite: Rework](#plan-for-suite-rework)
Status keywords, written only on a pause or a rework. Each Movement carries exactly one keyword at any moment:
- `Pending`: not entered yet, the starting keyword
- `Done`: closed Working
- `Halted`: stopped, awaiting rework
- `Dropped`: removed by rework
##### Movement Parties in Execution
For a user Movement, never do the work yourself. Guide interactively:
1. Movement In: say the Movement is theirs and its goal
2. give one step at a time; wait for their report before the next
3. halt per [Plan for Suite: Rework](#plan-for-suite-rework) if a report contradicts the Plan
4. settle the End State by their confirmation or your check, and say which
5. Movement Out once it holds
For another party, hand over steps and End State, await its report, then verify.
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
#### {[Claude:Skill] Usage}
Invoke the skill chosen for this run — `cascade-all-movements` or `halt-each-movement` — via `Skill` tool.
For each Movement's git commit, invoke `commit-sense` via `Skill` tool.
When halting for [Plan for Suite: Rework](#plan-for-suite-rework), invoke `rework-plan-for-suite` via `Skill` tool.
#### {[Claude:AskUserQuestion] Usage}
use `AskUserQuestion` tool to confirm each step or the End State of a user Movement, carrying likely replies as options
#### {[Claude:PushNotification] Usage}
Call `PushNotification` when the entire Suite is completed.
Write 1 line: emoji + Suite name
```text
🏁 Auth Refactor
```
#### {[git] Usage}
Each Movement lands as one git commit, performed as the chosen skill directs. A Movement that changes no workspace file, such as a user Movement, commits nothing.
### Plan for Suite: Rework
Halt the moment reality stops matching the Plan — a bug, a false assumption, a wrong or unnecessary Movement, unaccounted-for work, a user redirect, anything unanticipated. Never work around it.
1. present the finding: the Plan's assumption, the reality, and the cost to the Movements still ahead
2. rewrite the Plan whole — edit it in place, or author an entirely new file — never a diff, excerpt, or the rework alone. Keep completed Movements untouched and numbered; revise, remove, or add the rest as the finding demands
3. set every Movement's Status keyword per [Bar 2: Write the Plan](#bar-2-write-the-plan), so the file reads cold as exactly how far the run got and what the finding cost
4. never renumber to make room. A split Movement keeps its number and gains sub-Movements beneath it — `Movement 1` becomes `Movement 1.1` and `Movement 1.2`
5. present the revised Plan and hold for approval, as in [Bar 2: Write the Plan](#bar-2-write-the-plan)
6. once approved, Movement In to the earliest unfinished Movement, and not sooner
#### {[Claude:Enter/ExitPlanMode] Usage}
Immediate `EnterPlanMode` tool on halt,
and present the revised plan to user thru `ExitPlanMode` tool
#### {[Claude:AskUserQuestion] Usage}
use `AskUserQuestion` tool to ask user during the rework