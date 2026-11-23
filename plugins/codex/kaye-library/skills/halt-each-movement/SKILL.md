---
name: halt-each-movement
description: Stops after 1 Movement, waits for user to open next Turn
when_to_use: Trigger on "halt after each Movement", "one Movement at a time", "stop after every step", or "let me review between Movements".
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
## Halt Each Movement
Stop the Turn once 1 Movement is done; the next Movement begins only when user opens a new Turn.
1. Turn start
2. perform tasks of Movement
3. **Movement-Turn Dispatch**
4. Turn stop
5. user says "continue" or "c"
6. next Turn start
7. repeat from step 2, one Movement per Turn, until no Movement remains
**Movement-Turn Dispatch**: end the Turn with a [Turn Progress Dispatch](#turn-progress-dispatch), each line prefixed per [Movement Notation](#movement-notation):
```
🎏 🧩3\7 Rewrote the Entry Point
🧭 🧩4\7 Wire Up the Config Loader
```
Except when the entire Suite is completed — then name the Suite instead:
```
🏁 Auth Refactor
```
### {[git] Usage}
Index the Movement's edits before the Turn stop. Commit them at the next Turn start, once user approves (eg "git commit" or "g").