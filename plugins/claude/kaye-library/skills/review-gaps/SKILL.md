---
name: review-gaps
description: Audits whole repository for gaps, drift, unfinished seams — anything that becomes user-visible bug on public release; marks every surviving gap with a Loud TT.
when_to_use: 'Pre-release audit requests: "gap review," "ready to ship?," "what''s missing," "review project state." Not single-diff or single-file review.'
metadata:
  version: 1.5.1
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
## Gap Review
Inspect the repository and surface every inconsistency, gap, or unfinished seam likely to become user-visible after a public release. Read docs (`README`, `CHANGELOG`, `CONTEXT`, `AGENTS`, `docs/`) as the *claimed* contract, then code, tests, and packaging metadata as the *actual* one — every divergence is a candidate finding. Apply [Coder](#coder) when reading code, so findings rest on project convention rather than generic expectation.
Read-only, with one exception: inserting a *Loud TT* at every newly found gap. Never fix a finding unless asked in a later turn.
- report only what the repository shows, never inferring from filename or convention
- uncited is not a finding. An absent thing cites the place that should hold it — the manifest, the entry point, the module that imports it
- on conflict, code is truth and the document is the defect
- flag judgment calls plainly rather than inflating their class
#### Using Triage Tags
Existing *TT* are prior discovery — read them first and let them narrow the sweep. Judge by meaning rather than tag name or proximity, and choose every new tag per [Triage Tags](#triage-tags).
- already described by a *TT* → not a new gap. Skip silently, no new *TT*, no findings entry
- partly described → report the remainder only, naming the covering *TT*
- never restate or re-tag an existing *TT*; read *Steady* and *Quiet TT* for Context only
- every gap that survives the check gets one *Loud TT* at its site, whatever its class. Nothing else inserted
#### Categories
- docs drift: dropped commands, flags, env vars, modules; broken links
- code gaps: stubs, `NotImplementedError`, unhandled branches, hardcoded paths, secrets
- interfaces: signatures against docstrings, hints, examples; dead arguments; duplicated schemas
- config: undocumented or unvalidated env vars; orphaned keys; undeclared binaries
- dependencies: missing or unused manifest entries; unpinned ranges; stale lockfile
- packaging: excluded sources; entry points to missing modules; `.gitignore` faults
- tests: untested public behavior; dead fixtures; skips over shipped features
#### Findings
Rank by release impact, not fix effort. Straddling two classes, take the lower.
- ⛔ Critical: ordinary user hits outright failure — broken install, missing module, crash on the happy path, exposed secret, stub
- ⚠️ Warning: contract violated under ordinary input, artifact still runs
- 📌 Hint: stale wording, cosmetic drift, latent risk
Emit these three sections only, in the order below. No verdict, preface, or closing note.
```markdown
## ⛔ Critical

### Declare the `cache` extra in the package manifest

`pyproject.toml:34`

`README.md:58` documents `pip install acme[cache]`, and `acme/store/redis.py:12` imports `redis` at module load.

No such extra exists, so the documented install resolves to nothing and the store raises `ModuleNotFoundError` on a clean environment.

##### 🔧Fix

add the extra with its `redis` pin, or drop the documented path and the module behind it

## ⚠️ Warning
(every finding of warning, structured as above)

## 📌 Hint
(every finding of hint, structured as above)
```
- one finding per root cause, never per occurrence. A single defect reaching many sites stays one finding, citing two or three representative sites and stating the full spread in prose
- title each finding with an imperative naming the defect, not the symptom
- cite `path:line` verbatim and clickable, adding further citations inline as the body needs them
- hold the body to 1–2 dense paragraphs: what the repository claims versus what it holds, and the scope affected
- keep 🔧Fix to one line of plain direction — no patch, no code, no steps