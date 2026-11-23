---
name: push-event-to-calendar
description: Adds an event to the user's outside calendar app or service, from a single supplied event or from an event list already organized in the conversation.
when_to_use: Trigger on "add this to my calendar," "put these events on my calendar," "schedule this," or once an event list has been assembled in conversation and needs to land on the calendar. Trigger even w/o explicit ask whenever a firm, dated event surfaces in conversation that the user would plausibly want on the calendar. Not for pulling or checking existing calendar events
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
## calendar management
Default sub-calendars, to adapt: replace or extend them with the user's own sub-calendars when given:
- Business (work matters at the user's own workplace: in-team information, vendor and client dealings, invoicing and billing, contracts and partnerships, and project and deal coordination)
- Career (job search and professional advancement: applications, recruiter outreach, interviews, offers, and job market activity)
- Education (academic life: coursework, instruction, evaluation, and the institutional matters that surround them)
- Entertainment (leisure and recreation consumed or attended for enjoyment, not tied to a specific relationship; example: a concert, a movie screening, a board game night)
- Faith (religious and fellowship life: worship, spiritual growth, and the practices that carry them)
- Optional (events the user may attend or skip without consequence, not yet firmly committed; example: a coffee invite with no RSVP given, a neighbor's open house)
- Private (personal life with a real individual, not a bot or organization: relationships, one-on-one contact, and the exchanges shared with them)
- Public (fallback sub-calendar for an event that matches no more specific sub-calendar; example: a city's fireworks show, a library's public lecture)
----
Aggressively replace the full form with its shorthand:
- asgn:assign,assignment
- hw:homework
- mtg:meeting
### Push Event to Calendar
Movement 1~2, in strict order: each fully finished, with nothing skipped or reordered, before the next begins.
- Movement 1: Build event table per [Event Table](#event-table). Present it to the user & hold: push no event before the user confirms; the user may pick a subset by id per [Alphabetical Sequence Numbering in Chat](#alphabetical-sequence-numbering-in-chat)
- Movement 2: Confirm w/ user, then push: call the Create or Update tool per event
Optional, below the table: a bullet per event needing extra detail.
##### Event Table
The table holds each event's state, never what to change on it.
Example:
```md
| id | Event | 📅 | 📍 | Calendar | Remark |
| --- | --- | --- | --- | --- | --- |
| ⓐ | Jazz Night at the Blue Room | R 08-28 20:00 | The Blue Room, 123 Main St | Entertainment | Live jazz w/ house quartet & guest vocalist |
| ⓑ | Thesis Workshop | R 08-28 14:00~16:00 | 🌐Zoom | Education | Moved from Thu to Fri |

- ⓐ Repeats weekly on Thu, starts 08-28, ends 10-30 · [Event Page](https://example.com/jazz-night)
- ⓑ 🌐 [Zoom Meeting](https://zoom.us/j/1234567890)
```