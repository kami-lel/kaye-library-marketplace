---
name: ready-release-version
description: 'Cuts a project release: brings `README.md`, `CREDITS.md`, `CHANGELOG.md`, `AGENTS.md`, `CONTEXT.md`, and `docs/` current, moves `[Unreleased]` changelog entries into a dated versioned section, and bumps the version across metadata files like `package.json`, `pyproject.toml`, `Cargo.toml`, or `setup.cfg`.'
when_to_use: Reach for this on release requests — "ship v1.2.3," "cut a release," "tag a version," "bump the version," "prep the release." Not for logging a single in-progress change (use the changelog-maintain skill) or landing a feature branch before merge (use the feature-landing skill).
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
# Projects
## Project Semantic Version
- **core:** `major.minor.patch` / `x.y.z`
- pre-release: append `-` plus dot-separated identifiers, e.g. `x.y.z-alpha`, `x.y.z-alpha.2`. identifiers must use `[0-9a-z-]` only; no uppercase, no empty identifiers.
- build: append `+` plus dot-separated identifiers, e.g. `x.y.z+build.1`, `x.y.z-alpha+build.1`; identifiers must use `[0-9A-Za-z-]` only
### Semantic Version Extended
##### common pre-releases
- pre-releases types: `alpha`, `beta`, `rc`
- first pre-release: use unnumbered form, e.g. `1.0.0-alpha`.
- next pre-releases: start at `.2`, e.g. `1.0.0-alpha.2`, `1.0.0-alpha.3`, **do not use:** `1.0.0-alpha.1`
- pre-release patch: e.g. `1.0.0-alpha.2.1`
##### common build metadata
- `1.0.0+Win`, `1.0.0+mac`, `1.0.0+linux`: builds for different OS
- `0.5.0+2026-01-01-1234`, `1.0.0-alpha.2+2026-01-01`: date / date-time builds
##### development stage examples
- toy/prototypes: `0.1.z`~`0.4.z`
- Vertical Slice (VS): `0.5.z`~`0.8.z`
- pre-alpha: `0.9.z`
- alpha: `1.0.0-alpha`, `1.0.0-alpha.2`, ~~
- beta: `1.0.0-beta`, `1.0.0-beta.2`, ~~
- Release Candidate (RC): `1.0.0-rc`, `1.0.0-rc.2`
- first Stable Release: `1.0.0`
## Ready for Version Release
Cut a new release: bring all docs current, finalize the changelog, and bump the project version.
#### Movement 1: Decide Release Version and Date
- require both a version number and a release date; if either is missing, ask the user before proceeding
- the version must match [Project Semantic Version](#project-semantic-version)
#### Movement 2: Maintain the README and CREDITS
Run each in turn, skipping any whose file the repository lacks:
- [Maintain README](#maintain-readme): overview, features, setup, usage, version-dependent details
- [Maintain CREDITS](#maintain-credits): third-party assets added, moved, or removed since the last release
#### Movement 3: Maintain the Docs Directory
Run [Maintain Repository Docs](#maintain-repository-docs): affected files under `docs/`.
#### Movement 4: Condense AGENTS and CONTEXT
Run [Condense AGENTS and CONTEXT](#condense-agents-and-context): changed commands, conventions, constraints, architecture.
While in `CONTEXT.md`, prune as well as update: keep only what describes the released state, and cut superseded plans, stale notes, and history no longer worth a reader's time. The file should end up smaller, not just newer.
#### Movement 5: Condense and Close Out the Changelog
1. run [Condense CHANGELOG](#condense-changelog) to reword `[Unreleased]` entries into changelog style and settle any Admonitions for Breaks and Hazards
2. move every now-condensed `[Unreleased]` entry, admonitions included, into a new versioned section headed with the version and date from Movement 1, keeping only non-empty subsections
3. leave a fresh `[Unreleased]` section above it, carrying every standard subsection heading with no entries beneath
4. update the GitHub comparison links so every version, including the new tag, stays referenced
#### Movement 6: Bump the Repository Version
Set the version to match Movement 1 exactly, in whichever metadata files apply — `setup.cfg`, `pyproject.toml`, `package.json`, `Cargo.toml`, and the like.
### {[Claude:Skill] Usage}
Invoke `maintain-readme`, `maintain-credits`, `condense-changelog`, `condense-agents-and-context`, and `maintain-repo-docs` skills via `Skill` tool.
### {[Claude:AskUserQuestion] Usage}
- if version number or release date is **missing**, use `AskUserQuestion` to ask user before proceeding