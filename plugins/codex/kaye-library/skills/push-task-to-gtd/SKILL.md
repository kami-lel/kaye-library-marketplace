---
name: push-task-to-gtd
description: Adds tasks to user's GTD app, each assigned a project & an Eisenhower quadrant, from 1 supplied task or a task list organized in conversation.
when_to_use: Trigger on "add to my tasks," "put on my to-do list," "remind me to," or once a task list needs to land in GTD. Trigger even w/o explicit ask when a firm to-do surfaces that user would plausibly track. Not for pulling or checking existing tasks
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
# Secretary
## getting-things-done management
### Push Task to GTD
Movement 1~2, in strict order: each fully finished, with nothing skipped or reordered, before the next begins.
- Movement 1: Assign each task 1 Project & 1 Quadrant, then build task table per [Task Table](#task-table). Present it to the user & hold: push no task before the user confirms; the user may pick a subset by id per [Alphabetical Sequence Numbering in Chat](#alphabetical-sequence-numbering-in-chat)
- Movement 2: Confirm w/ user, then push: call the Create or Update tool per task
Optional, below the table: a bullet per task needing extra detail.
----
Default projects, to adapt: replace or extend them with the user's own GTD projects when given. 1 per task, never blank: first fit in list order:
1. Learn (self-directed learning of a skill or tool set outside institutions: self-teaching, tutorials, books, and courses)
2. Work (non-institutional work that makes something: the user's own development projects, prototypes, tooling, and interest-driven pursuits; learning a skill or tool for it belongs to Learn)
3. Business (work matters at the user's own workplace: in-team information, vendor and client dealings, invoicing and billing, contracts and partnerships, and project and deal coordination)
4. Education (academic life: coursework, instruction, evaluation, and the institutional matters that surround them)
5. Career (job search and professional advancement: applications, recruiter outreach, interviews, offers, and job market activity)
6. Admin (Administration: government correspondence, visa/immigration, tax filings, legal notices, and banking; medical and insurance matters; school enrollment and tuition; and company HR, payroll, and benefits)
7. Purchase (a list of things the user wants to buy)
8. Routine (recurring, repetitive tasks that fit none of the specific entries above)
9. Inbox (default entry: anything that fits none of the entries above)
----
Quadrants, 1 per task:
- 💎:Important (carries significant consequence or value toward a goal or priority, independent of timing: long-term impact, alignment with a core objective, or work that enables or unblocks other work)
- 🚨:Urgent (demands prompt action because delay itself imposes a cost: a closing time window, an escalating consequence, or a dependency that leaves other work blocked while it waits)
- 💎🚨:Important & Urgent
----
Aggressively replace the full form with its shorthand:
- asgn:assign,assignment
- hw:homework
- mtg:meeting
##### Task Table
The table holds each task's state, never what to change on it.
Quadrant cell: the quadrant's emoji
Deadline cell: date alone w/o time; empty w/o date/time
Example:
```md
| id | Task | 🎯 | Project | Quadrant | Remark |
| --- | --- | --- | --- | --- | --- |
| ⓐ | Submit thesis draft | U 08-30 | Education | 💎🚨 | Advisor review follows |
| ⓑ | Buy printer ink |  | Persistent | 🚨 | Repeats weekly |

- ⓐ Checklist: outline, citations, abstract · [Draft Doc](https://example.com/thesis-draft)
```