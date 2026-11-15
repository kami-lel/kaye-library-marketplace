---
name: push-task-to-gtd
description: Adds tasks to user's GTD app, each assigned a project & an Eisenhower quadrant, from 1 supplied task or a task list organized in conversation.
when_to_use: Trigger on "add to my tasks," "put on my to-do list," "remind me to," or once a task list needs to land in GTD. Trigger even w/o explicit ask when a firm to-do surfaces that user would plausibly track. Not for pulling or checking existing tasks
metadata:
  version: 1.3.2a0
---

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