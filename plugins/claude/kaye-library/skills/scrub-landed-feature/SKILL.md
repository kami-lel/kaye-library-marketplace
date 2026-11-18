---
name: scrub-landed-feature
description: 'Scrubs up after a feature branch lands on `dev`: reports the landing, then, each on approval, pushes `dev`, uproots the branch''s linked worktree, and deletes the merged branch.'
when_to_use: 'Reach for this once a feature branch is merged into `dev`: "clean up after the merge," "push dev and delete the branch," "scrub the landed feature." Not for merging the branch itself (use the land-feature skill) or pruning many merged branches at once (use the prune-merged-branches skill).'
metadata:
  version: 1.5.0
---

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
### {[Claude:Skill] Usage}
Invoke `uproot-linked-wt` skill via `Skill` tool.