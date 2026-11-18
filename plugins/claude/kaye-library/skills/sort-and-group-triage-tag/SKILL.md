---
name: sort-and-group-triage-tag
description: Reorders existing triage tags into grouped blocks — tier from Loud to Quiet, then meaning from bug to fixme, todo, hack. Position only, nothing else changes.
when_to_use: Reach for this on "sort the triage tags," "group them by tier," "put the loud ones together," or after a sweep appends new tags to a block. Not for writing a tag or fixing what one marks.
metadata:
  version: 1.5.0
---

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