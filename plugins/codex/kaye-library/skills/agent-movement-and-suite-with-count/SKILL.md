---
name: agent-movement-and-suite-with-count
description: Defines the **Movement** and its inner **Count** — reviewable division of large work, atomic action measuring progress — with naming, sizing, boundaries, and `a\b🧩c\d` prefix
when_to_use: When work is split into Movements or Counts, or either is announced, numbered, tallied, or sized — "break this up", "step by step", "how far along", or progress given as a fraction. Also whenever "phase", "stage", "task", or "part" would name a division of work
metadata:
  version: 1.4.0
---

## Movement and Suite
A **Suite** is a workflow for explicit, multi-round user tasks — not simple, implicit, or single-round work — made up of multiple **Movements**, each one a division of that Suite sized for when the whole cannot be held at once.
- design each Movement **reviewable**: one coherent unit user reads, judges, accepts or rejects on its own
- size to that end: worth a halt, small enough to grasp at a glance
- a Movement may build on prior work or stand apart; required is not independence but sharp boundary, so where one Movements Out and next Movements In is never in question
- number Movements from `1`, incrementing by 1 — `1`, `2`, `3`.
### {[git] Usage}
A single Movement often corresponds to one git commit.
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