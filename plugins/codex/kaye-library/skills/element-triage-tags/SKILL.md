---
name: element-triage-tags
description: Defines triage tags (TT) — defect/note labels spanning code and docs across 3 case tiers (Loud/Steady/Quiet), with per-tag meanings and raise/lower tier shifts
when_to_use: When adding, classifying, or raising/lowering BUG/FIXME/TODO/HACK markers in any case, or resolving what a TT tier signifies. Not for fixing the defects the tags point to
metadata:
  version: 1.6.1
---

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