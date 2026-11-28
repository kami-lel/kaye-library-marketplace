---
name: halt-each-movement
description: Stops the Main Voice after 1 Movement, waits for user to open next Turn
when_to_use: Trigger on "halt after each Movement", "one Movement at a time", "stop after every step", or "let me review between Movements".
metadata:
  version: 1.6.2
---

## Halt Each Movement
This governs the Main Voice only: its Movements halt, an instrumental Voice never does.
Stop the Turn once 1 Movement is done; the next Movement begins only when user opens a new Turn.
1. Turn start
2. perform tasks of Movement
3. **Movement-Turn Dispatch**
4. Turn stop
5. user says "continue" or "c"
6. next Turn start
7. repeat from step 2, one Movement per Turn, until no Movement remains
An instrumental Voice runs whole in either mode, never halted inside, whatever halt mode its own session loads. Its report tells you it has ended: returned by its subagent, sent from its session, or relayed by the user. Once the report arrives, merge it back and halt there as at a Movement's close, so its review comes then.
**Movement-Turn Dispatch**: end the Turn with a [Turn Progress Dispatch](#turn-progress-dispatch), each line prefixed per [Movement Notation](#movement-notation) and [Dispatch Marks](#dispatch-marks):
```
🎏 🧩3\7 Rewrote the Entry Point
🧭 🧩4 Wire Up the Config Loader
```
At an instrumental Voice's merge back:
```
🎌 Violin Test Fixtures Merged Back
🧭 🧩5 Rebuild the Entry Point
```
Except when the entire Suite is completed — then name the Suite instead:
```
🏁 Auth Refactor
```
### {[git] Usage}
Index the Movement's edits before the Turn stop. Commit them at the next Turn start, once user approves (eg "git commit" or "g").
Merge a finished instrumental Voice's instrumental branch into the feature branch before the Turn stop that marks it 🎌.
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