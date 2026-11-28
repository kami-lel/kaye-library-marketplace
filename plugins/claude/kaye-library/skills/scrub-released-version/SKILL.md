---
name: scrub-released-version
description: 'Scrubs up after a version release: reports the release, then, each on approval, pushes `main` and its `v` tag, prunes merged branches, fast-forwards `dev` to `main`, and bumps `dev` to the next patch alpha.'
when_to_use: 'Reach for this once a release is merged into `main` and tagged: "push the release," "clean up after the release," "sync dev with main," "open the next alpha on dev." Not for cutting the release itself (use the release-version skill) or pruning branches alone (use the prune-merged-branches skill).'
metadata:
  version: 1.6.1
---

## Movement, Voice, and Suite
An explicit, multi-round user task runs as 3 nested units: Suite, Voice, and Movement. Never use them for simple, implicit, or single-round work.
**Suite**: the whole workflow for 1 such task
- holds 1+ Voices, the Main Voice always among them
- works on its feature branch, often 1 Suite = 1 feature branch, which every voice branch merges back into
- completes once every Voice has merged back and no Movement remains
**Voice**: 1 line of Movements within a Suite, run in order
- the **Main Voice** is the Suite's own line, marked 🧩: every Movement outside the other Voices, user Movements included; the main session runs it, never a subagent or another session
- every other Voice is an **instrumental Voice**: agent only, with no user Movement, approval, or question inside it
- an instrumental Voice runs in 1 of 2 modes, both following `solo-voice`: soloed by a subagent of the main session, or run in its own session
- each instrumental Voice runs in parallel with the Main Voice and the rest, on its own voice branch and linked worktree; its voice branch is cut from the feature branch and merges back into it once its Movements are done
- an instrument emoji therefore always marks an instrumental Voice
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
- voice (line of Movements within a Suite; any but the Main Voice is an instrumental Voice: agent only, soloed by a subagent or run in its own session, in parallel on its voice branch, then merged back into the feature branch)
- suite (unit contains 1+ Voices)
in general: Round < Movement < Voice < Suite
### {[git] Usage}
Commit each Movement's edits as exactly one git commit: 1 Movement = 1 commit.
Often 1 Suite = 1 feature branch. 1 Voice = 1 voice branch, cut from the feature branch and merged back into it.
### {[Claude:TodoWrite] Usage}
One `TodoWrite` entry per Movement in the Suite, every Voice included — 1:1, never merged or split. List the Main Voice's entries first, then each instrumental Voice's in instrument order, each Voice's in Movement order.
- `content`: prefix + Movement imperative
- `activeForm`: prefix + present continuous
Status flow: `pending` at Seed (before Movement 1 opens) → `in_progress` on Open → `completed` on Close, once Working state is verified.
Rules:
- exactly 1 entry `in_progress` in the Main Voice, plus 1 per open instrumental Voice
- Movement added or dropped mid-Suite: edit the array in the call that closes the current Movement
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
#### {[Claude:TodoWrite] Usage}
`TodoWrite` Examples, with prefix `🧩a SUMMARY` or `🎻a SUMMARY`
Seed:
```json
{
  "todos": [
    {
      "content": "🧩1 Rewrite the Entry Point",
      "status": "pending",
      "activeForm": "🧩1 Rewriting the Entry Point"
    },
    {
      "content": "🧩2 Move the Parser to Its Own Module",
      "status": "pending",
      "activeForm": "🧩2 Moving the Parser to Its Own Module"
    },
    {
      "content": "🧩3 Wire the Parser Into the Entry Point",
      "status": "pending",
      "activeForm": "🧩3 Wiring the Parser Into the Entry Point"
    },
    {
      "content": "🎻1 Update the Test Fixtures",
      "status": "pending",
      "activeForm": "🎻1 Updating the Test Fixtures"
    },
    {
      "content": "🎻2 Add Parser Tests",
      "status": "pending",
      "activeForm": "🎻2 Adding Parser Tests"
    }
  ]
}
```
Open Movement 2 while the Violin Voice runs — resend whole array, 2 statuses change:
```json
{
  "todos": [
    {
      "content": "🧩1 Rewrite the Entry Point",
      "status": "completed",
      "activeForm": "🧩1 Rewriting the Entry Point"
    },
    {
      "content": "🧩2 🥁 Move the Parser to Its Own Module",
      "status": "in_progress",
      "activeForm": "🧩2 🥁 Moving the Parser to Its Own Module"
    },
    {
      "content": "🧩3 Wire the Parser Into the Entry Point",
      "status": "pending",
      "activeForm": "🧩3 Wiring the Parser Into the Entry Point"
    },
    {
      "content": "🎻1 Update the Test Fixtures",
      "status": "in_progress",
      "activeForm": "🎻1 Updating the Test Fixtures"
    },
    {
      "content": "🎻2 Add Parser Tests",
      "status": "pending",
      "activeForm": "🎻2 Adding Parser Tests"
    }
  ]
}
```
# Projects
## Project Semantic Version
- **core:** `major.minor.patch` / `x.y.z`
- pre-release: append `-` plus dot-separated identifiers, e.g. `x.y.z-alpha`, `x.y.z-alpha.2`. identifiers must use `[0-9a-z-]` only; no uppercase, no empty identifiers.
- build: append `+` plus dot-separated identifiers, e.g. `x.y.z+build.1`, `x.y.z-alpha+build.1`; identifiers must use `[0-9A-Za-z-]` only
### semantic version bump
A **semantic version bump** is the part of the version core (major, minor, patch) the new version raised over the old one. Compare the two cores:
| Bump | When |
|---|---|
| Major | `x` is higher |
| Minor | `y` is higher, `x` equal |
| Patch | `z` is higher, `x` and `y` equal |
Where none holds (equal, lower, or either side not `x.y.z`), the version has no bump.
### Semantic Version Title
Write the title of a version release as `BUMP TYPE VERSION`:
1. Find BUMP: compare the new version with the old one, per [semantic version bump](#semantic-version-bump).
2. Find TYPE: look up the new version in the table below.
Drop BUMP when the new version has no bump. TYPE is never dropped.
##### release type
Check the new version against the rows from top to bottom. Stop at the first match.
| Version | Type |
|---|---|
| contains `-alpha` | Alpha Release |
| contains `-beta` | Beta Release |
| contains `-rc` | Release Candidate |
| `0.9.z` | Pre-Alpha Release |
| `0.5.z`~`0.8.z`, only when Vertical Slice is enabled | Vertical Slice |
| `0.y.z` | Prototype |
| `x.y.z` | Release |
##### examples
| New | Old | Title |
|---|---|---|
| `0.3.2` | `0.3.1` | `Patch Prototype 0.3.2` |
| `0.9.3` | `0.9.2` | `Patch Pre-Alpha Release 0.9.3` |
| `1.0.0-beta.2` | `0.9.0` | `Major Beta Release 1.0.0-beta.2` |
| `1.0.0-rc` | `1.0.0-beta.2` | `Release Candidate 1.0.0-rc` |
| `1.1.0` | `1.0.0` | `Minor Release 1.1.0` |
## Scrub After Version Release
Once the release is merged into `main` and tagged, scrub what it left behind: publish `main` and the tag, prune merged branches, bring `dev` level with `main`, and open the next version on `dev`. Each step waits for the user's approval, since a push publishes and a pruned branch cannot be recovered by name.
Learn the release first:
- version: settled in the conversation, else the `v` tag on `main`'s tip, read with `git describe --tags --exact-match main`
- title: that version's [Semantic Version Title](#semantic-version-title), eg `Minor Release 1.1.0`
#### Movement 1: Report and Ask Approval
Reply as below, asking 4 approvals: push `main` and the tag, prune merged branches, naming each branch to prune (the candidates of [Prune Merged Branches](#prune-merged-branches)), fast-forward `dev` to `main`, local and remote, and bump `dev` to the next alpha, naming that version.
The next alpha raises the released patch by 1 and appends `-alpha`, eg `1.2.5` opens `1.2.6-alpha`, so `dev` never claims a released version.
<post-release-output-example>
🚩🐙 Minor Release 1.1.0
✍️ ⓑ push `main` and `v1.1.0` to origin?
✍️ ⓒ prune merged branches `add-search-filter`, `fix-login-redirect`?
✍️ ⓓ fast-forward `dev` to `main`, local and origin?
✍️ ⓔ bump `dev` to `1.1.1-alpha`, local and origin?
ⓐ all of above
</post-release-output-example>
#### Movement 2: Push, Prune, and Sync Dev
Run only the approved actions, in order; ⓐ approves all four:
- ⓑ `git push origin main vVERSION`
- ⓒ invoke `prune-merged-branches`
- ⓓ fast-forward `dev` to `main`, local and origin; if it cannot fast-forward, report in one line and stop
- ⓔ only after ⓓ succeeds (else skip, saying why): on `dev`, set the next alpha in every version metadata file, commit per [Commit Sense](#commit-sense), then `git push origin dev`
Reply once, after all are done:
<post-push-prune-output-example>
🚩🐙 pushed `main` and `v1.1.0` to origin
🚩🐙 pruned `add-search-filter`, `fix-login-redirect`
🚩🐙 fast-forwarded `dev` to `main`, local and origin
🚩🐙 bumped `dev` to `1.1.1-alpha`, local and origin
</post-push-prune-output-example>
### {[Claude:Skill] Usage}
Invoke `prune-merged-branches` and `commit-sense` skills via `Skill` tool.