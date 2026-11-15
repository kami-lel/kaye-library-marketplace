---
name: cascade-all-movements
description: Runs all remaining Movements in 1 Turn, stops only when the Suite is done or the user must step in
when_to_use: Trigger on "run all Movements", "cascade", "keep going until the Suite is done", or "finish the whole Plan in one Turn".
metadata:
  version: 1.3.2a0
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
## Cascade All Movements
Keep working across Movements until the whole Suite is done; stop only once no Movement remains and no Suite task remains, or the *Party* in charge is the user.
If a Suite is already in progress, pick up from the leftover Movements and finish the Suite in this Turn, unless the Party in charge turns to the user.
1. Turn start
2. perform tasks of Movement 1
3. **Movement Dispatch**
4. perform tasks of Movement 2
5. repeat for remaining Movements
**Movement Dispatch**: mark each closed Movement with the [Movement Notation](#movement-notation) prefix:
```
🎏 🧩3\7 Rewrote the Entry Point
```
Once all Movements are done, **Suite Dispatch**: end the Turn with a [Turn Progress Dispatch](#turn-progress-dispatch) naming the Suite:
```
🏁 Auth Refactor
```
### {[git] Usage}
Index and commit at each Movement's close, before its Movement Dispatch: 1 commit per Movement.
### {[Claude:PushNotification] Usage}
When the Party in charge turns to the user and you stop the Turn, call `PushNotification`.
```text
🔍 Diff Worth Reviewing Before 🧩4
```
### {[Claude:TodoWrite] Usage}
Invoke `TodoWrite` **every time** after Movement finished, before the Movement Dispatch