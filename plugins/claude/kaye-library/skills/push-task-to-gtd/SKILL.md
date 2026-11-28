---
name: push-task-to-gtd
description: Adds tasks to user's GTD app, each assigned a project & an Eisenhower quadrant, from 1 supplied task or a task list organized in conversation.
when_to_use: Trigger on "add to my tasks," "put on my to-do list," "remind me to," or once a task list needs to land in GTD. Trigger even w/o explicit ask when a firm to-do surfaces that user would plausibly track. Not for pulling or checking existing tasks
metadata:
  version: 1.6.1
---

## Movement, Voice, and Suite
An explicit, multi-round user task runs as 3 nested units: Suite, Voice, and Movement. Never use them for simple, implicit, or single-round work.
**Suite**: the whole workflow for 1 such task
- holds 1+ Voices, the Main Voice always among them
- works on its feature branch, often 1 Suite = 1 feature branch, which every voice branch merges back into
- completes once every Voice has merged back and no Movement remains
**Voice**: 1 line of Movements within a Suite, run in order
- the **Main Voice** is the Suite's own line, marked 🧩: every Movement outside the other Voices, user Movements included; the main session runs it, never a subagent or another session
- every other Voice is an **instrumental Voice**: agent only, with no user Movement, approval, or question inside it
- an instrumental Voice runs in 1 of 2 modes, both following `solo-voice`: soloed by a subagent of the main session, or run in its own session
- each instrumental Voice runs in parallel with the Main Voice and the rest, on its own voice branch and linked worktree; its voice branch is cut from the feature branch and merges back into it once its Movements are done
- an instrument emoji therefore always marks an instrumental Voice
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
- voice (line of Movements within a Suite; any but the Main Voice is an instrumental Voice: agent only, soloed by a subagent or run in its own session, in parallel on its voice branch, then merged back into the feature branch)
- suite (unit contains 1+ Voices)
in general: Round < Movement < Voice < Suite
### {[git] Usage}
Commit each Movement's edits as exactly one git commit: 1 Movement = 1 commit.
Often 1 Suite = 1 feature branch. 1 Voice = 1 voice branch, cut from the feature branch and merged back into it.
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
#### {[Claude:TickTick] Usage}
Movement 2: Call `TickTick:create_task` per new task: carry title, due date, project, quadrant & brief description from source. Quadrant sets `priority`: 💎🚨 → 5, 💎 → 3, 🚨 → 1, ➖ → 0; same on batch & update calls.
Several new tasks at once: call `TickTick:batch_add_tasks` instead
Task exists already, detail only changed: call `TickTick:update_task` instead; several at once: `TickTick:batch_update_tasks`
Project unknown: call `TickTick:list_projects` first