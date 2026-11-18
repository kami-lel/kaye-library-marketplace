---
name: rework-plan-for-suite
description: 'Reworks running Plan file when reality stops matching it: halts, rewrites Plan, holds for approval before work resumes'
when_to_use: 'Mid-run on bug, false assumption, wrong or unnecessary Movement, unaccounted-for work, user redirect, workspace mismatch on resume — even unprompted. Triggers: rework the Plan, replan, Plan no longer fits. Not for drafting Plans (`plan-for-suite`) or running Movements (`execute-plan-for-suite`)'
metadata:
  version: 1.5.0
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