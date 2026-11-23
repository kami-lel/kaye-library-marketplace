---
name: sync-unit-test
description: Reconciles a failing test suite with a codebase's changed behavior — realigning stale assertions, fixtures, and baselines to the new contract, and surfacing the failures where the code, not the test, may be what drifted.
when_to_use: Trigger when tests fail after a refactor, API change, or redesign — "tests broke after my change," "sync the tests," "re-baseline snapshots." Not for writing a suite for untested code.
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
### {[Claude:TodoWrite] Usage}
One `TodoWrite` entry per Movement in the Suite — 1:1, never merged or split. Entry index gives Movement number `a`; array length gives total `b`.
- `content`: prefix + Movement imperative
- `activeForm`: prefix + present continuous
Status flow: `pending` at Seed (before Movement 1 opens) → `in_progress` on Open → `completed` on Close, once Working state is verified.
Rules:
- exactly 1 entry `in_progress` at a time
- Movement added or dropped mid-Suite: edit the array in the call that closes the current Movement, and rewrite every prefix to the new `b`
### Movement with Count
A **Count** is any countable atomic unit that may exist within a Movement — files affected, bugs to fix, tests to implement. What a Count is depends on the usage. One Movement holds one or more Counts. Counts measure progress only: never halted at
individually, and a Movement of many Counts still closes as one Movement.
----
Every mention of a Movement takes the form `a\b🧩c\d SUMMARY`:
- `a` Counts closed to date — all Counts of prior Movements, plus this Movement's own
- `b` total Counts across all Movements
- `c` current Movement number
- `d` total Movement count
- `SUMMARY` short description of the Movement, in [Title Case](#letter-case-title-case)
*Example — 3 Movements holding 4, 5, 3 Counts, 12 total:*
```
4\12🧩1\3 Cleared First 4
9\12🧩2\3 5 More Closed
12\12🧩3\3 Last 3
```
#### {[Claude:TodoWrite] Usage}
`TodoWrite` Examples, with prefix `a\b🧩c\d SUMMARY`
Seed:
```json
{
  "todos": [
    {
      "content": "4\\12🧩1\\3 Rewrite the Entry Point",
      "status": "pending",
      "activeForm": "4\\12🧩1\\3 Rewriting the Entry Point"
    },
    {
      "content": "9\\12🧩2\\3 Move the Parser to Its Own Module",
      "status": "pending",
      "activeForm": "9\\12🧩2\\3 Moving the Parser to Its Own Module"
    },
    {
      "content": "12\\12🧩3\\3 Update the Test Fixtures",
      "status": "pending",
      "activeForm": "12\\12🧩3\\3 Updating the Test Fixtures"
    }
  ]
}
```
Open Movement 2 — resend whole array, 1 status changes:
```json
{
  "todos": [
    {
      "content": "4\\12🧩1\\3 Rewrite the Entry Point",
      "status": "completed",
      "activeForm": "4\\12🧩1\\3 Rewriting the Entry Point"
    },
    {
      "content": "9\\12🧩2\\3 🥁 Move the Parser to Its Own Module",
      "status": "in_progress",
      "activeForm": "9\\12🧩2\\3 🥁 Moving the Parser to Its Own Module"
    },
    {
      "content": "12\\12🧩3\\3 Update the Test Fixtures",
      "status": "pending",
      "activeForm": "12\\12🧩3\\3 Updating the Test Fixtures"
    }
  ]
}
```
## Triage Tags
Labels for defects and related notes across code and docs; refer to them as *triage tags* or *TT*.
Each tag comes in three tiers by letter case:
- *Loud* — all-caps: `BUG`, `FIXME`, `TODO`, `HACK`
- *Steady* — capitalized: `Bug`, `Fixme`, `Todo`, `Hack`
- *Quiet* — lowercase: `bug`, `fixme`, `todo`, `hack`
Shifting to a louder tier is **raise**; to a quieter tier is **lower**.
### Triage Tags Meanings
- `BUG` — discovered defects causing errors or unexpected behavior
- `FIXME` — content that is wrong, inefficient, unclear, or otherwise improvable
- `TODO` — intentionally incomplete work or placeholders for later
- `HACK` — temporary workarounds expected to be removed before release
### Sort and Group Triage Tag
On invocation, collect every *TT* in scope and rewrite it into one grouped, sorted arrangement. Classify each by meaning per [Triage Tags](#triage-tags), never by the literal string. Reorder only — never reword, re-tier, merge, or act on what a tag describes.
##### Order
Sort on two keys, tier before meaning.
- tier, loudest first: Loud, Steady, Quiet
- meaning, within each tier: bug, fixme, todo, hack
- ties hold their original relative order, so unrelated tags never shuffle
##### Grouping
- each tier forms one contiguous block, nothing interleaved
- within a tier, each meaning forms its own run — every Loud bug adjacent, then every Loud fixme, on down
## Sync Unit Test
The suite and the codebase have fallen out of agreement. Restore it.
If an environment or tool setup issue arises during test execution, stop immediately and ask the user how to resolve it.
Three Movements: triage, consult, repair. Repair runs as Movements and Counts, per [Movement and Suite](#movement-and-suite); triage determines their number.
#### Movement 1: triage first
Classify every failure before any edit. A *TT* on or near a failing test is Context, per [Triage Tags](#triage-tags) — never insert, edit, or resolve one here.
- **stale**: behavior changed on purpose; the test is what drifted. Read the diff and commits to learn the New contract
- **regression or ambiguous**: the codebase may have drifted instead, or the intended contract won't resolve from history
Count the stale failures. Ten or fewer: one Movement, one Count per test. More than ten: group first, one Group per shared Cause — each Group becomes a Movement, each test in it a Count. Name Groups by Cause, not file; keep each small enough to review in one pass; split any Group that spans unrelated Causes. Ungroupable tests form a final Group, repaired one at a time.
Each regression or ambiguous failure gets its own Movement (one Count, unless its answer needs more), numbered ahead of the stale Movements.
Movement 1 ends with findings: counts, Groups and their Causes, each regression or ambiguous failure named with what's unclear about it, and the resulting Movement plan — total Movements and total Counts, so numbering can start from the first Count.
#### Movement 2: consult user
Skip this Movement when triage found only stale tests.
Otherwise, you must stop and halt all work before Movement 1 opens — no exceptions. Ask about intended behavior, never about the test itself — what the contract should be, and which side must move. Present the plausible resolutions plainly, one failure at a time, and wait. Editing is forbidden until every question is answered; never proceed on an assumed or guessed answer.
#### Movement 3: repair
Open Movement 1 only once every Movement 2 question is answered. Close one Movement before opening the next, each in a Working state: its tests pass, and nothing previously passing has broken.
Realign stale tests without asking again. Settle everything raised in Movement 2 to the answer given, and no further — including production-code edits where the user named that side.
- update expected values, fixtures, and mocks to the New contract
- rename tests still named for Removed behavior
- delete tests for behavior that's gone, stating Which and Why
- add tests where new behavior sits Uncovered
- re-baseline a snapshot only after reading Every changed line
- keep original intent — an error-path test still tests the Error path
Closed to you:
- editing production code to silence a stale test, or to settle anything Movement 2 didn't
- weakening an assertion, loosening a type check, widening a tolerance
- skipping, commenting out, or marking expected-failure instead of fixing
- accepting a snapshot unread, or touching a test that was passing
- reshaping the Movement plan silently — split, say so, and publish corrected totals instead
Report each Count as it lands: classification, which side moved, and why. When a Movement closes, name the tests it now leaves passing.
### {[Claude:AskUserQuestion] Usage}
Run Movement 2 through the `AskUserQuestion` tool, carrying plausible resolutions as options.
### {[Claude:ReportFindings] Usage}
At end of Movement 1, use `ReportFindings` tool to report all failed tests.
- one finding per failed file
- `category`: stale, regression or ambiguous
### {[Claude:TodoWrite] Usage}
During Movement 3: call `TodoWrite` when:
- Seed: before Movement 1 opens, show all repairing Movements
- after finish any Movement: present user the current status