---
name: scrub-landed-feature
description: 'Scrubs up after a feature branch lands on `dev`: reports the landing, then, each on approval, pushes `dev`, uproots the branch''s linked worktree, and deletes the merged branch.'
when_to_use: 'Reach for this once a feature branch is merged into `dev`: "clean up after the merge," "push dev and delete the branch," "scrub the landed feature." Not for merging the branch itself (use the land-feature skill) or pruning many merged branches at once (use the prune-merged-branches skill).'
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
# Git
## feature branch
A **feature branch** is a branch cut from `dev` to build one feature in isolation, then merged back.
Name it starting with a verb, never with a `feature/` prefix, eg `add-search-filter`, `fix-token-refresh`.
Assume local `HEAD` is the feature branch. Observe it with `git log dev..HEAD`: the commits it holds that `dev` lacks.
### discover feature branch
Learn what the finished [feature branch](#feature-branch) delivers and why:
- read the current conversation for what was built and why
- understand the change set from both sources: `git log dev..HEAD` and the `[Unreleased]` entries of `CHANGELOG.md`; fold them together so nothing is stated twice
- if the two together leave the change unclear, read the change directly: `git diff dev...HEAD`
### feature branch summary
Only for a Feature Landing: the body of its merge message, per [Commit Sense For Branch Merging](#commit-sense-for-branch-merging), and the wording of its pull request, per [Submit Pull Request](#submit-pull-request).
Given [Discover Feature Branch](#discover-feature-branch), write the summary the reviewer merging into `dev` decides from, so lead with the outcome:
- headline: one verb-first sentence on what the branch delivers
- changes: 2~5 bullets grouped by purpose, each saying what changed and why it matters
Write strictly in [Briefness Style](#style-guide-briefness-style),
and apply [Commentary Case](#letter-case-commentary-case) to every line
example:
```md
add status filter to Search page

- filter results by status: no full-list scan for open items
- persist chosen filter in URL: reload/shared link keeps view
```
#### {avoid}
Retelling commits or listing files.
## Scrub After Feature Landing
Once the [feature branch](#feature-branch) has landed on `dev`, scrub what it left behind: publish `dev`, then remove the merged branch and its linked worktree. Each step waits for the user's approval, since a push publishes and a deletion cannot be undone.
Learn the landing first:
- branch: named in the conversation, else the second parent of the merge commit at `dev`'s tip
- headline: the first line of the [feature branch summary](#feature-branch-summary) in that merge commit's message
#### Movement 1: Report and Ask Approval
Reply as below, asking up to 3 approvals: push `dev`; delete the feature branch (merged, so safe to drop); uproot its linked worktree, asked only when one holds the branch.
<post-landing-output-example>
🚩🐙 Feature Landed: add status filter to Search page
✍️ ⓑ push `dev` to origin?
✍️ ⓒ delete feature branch `add-search-filter`?
✍️ ⓓ uproot linked worktree `kaye-library-WT-add-search-filter`?
ⓐ all of above
</post-landing-output-example>
#### Movement 2: Push and Delete
Run only the approved actions, in order ⓑ, ⓓ, ⓒ, since Git refuses to delete a branch while a worktree holds it; ⓐ approves all three:
- ⓑ `git push origin dev`
- ⓒ `git branch -d FEATURE`, never `-D`
- ⓓ invoke `uproot-linked-wt`
Reply once, after all are done:
<post-push-delete-output-example>
🚩🐙 pushed `dev` to origin
🚩🐙 uprooted `kaye-library-WT-add-search-filter`
🚩🐙 deleted `add-search-filter`
</post-push-delete-output-example>