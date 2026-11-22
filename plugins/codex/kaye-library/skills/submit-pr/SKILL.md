---
name: submit-pr
description: Opens a pull request landing a feature branch on `dev`, after readying its docs, with the title and body drawn from the branch summary.
when_to_use: Trigger on "open a PR", "create a pull request", "submit this feature", "land this on dev", or `gh pr create`. Not for syncing docs alone before a merge (use `ready-land-feature`) or wording a merge commit (use `commit-sense-branch-merging`).
metadata:
  version: 1.5.1
---

# Style Guide
## Letter Case
### Letter Case Commentary Case
- begin 1st sentence with a lowercase letter; use standard sentence capitalization for the 2nd and subsequent sentences
- use [*Title Case*](#letter-case-title-case) for a few important words within a sentence
- the last sentence should not end with punctuation
example:
```
# this initializes the Variable
# check the Config. Validate the Filepath with the Tool. Process final result
```
## Style Guide Briefness Style
- write in **newspaper headlinese**, prioritize brevity over grammar
- use present for current, infinitive for planned
- omit articles (a, an, the) and helper verbs, use strong nouns, verbs
- compress with punctuation: colon, dash, comma, otherwise minimize, no terminal periods
- use numerals (use 2, not two), symbols, common abbreviations when unambiguous
- prefer active voice
- keep sentences short, direct, drop filler
Aggressively replace the full form with its shorthand:
- vs.:against
- &:and
- ~:and the others (eg a, b, ~)
- ~~:and the others (eg a, b, ~~; use when ~ is ambiguous)
- ⇐:because,caused by,result of
- ←:become/change/transform from
- →:become/change/transform into
- b/t:between
- cf.:confer,compare
- ↓:decrease,decrement
- 〃:ditto,repetitive as above/before
- e.g.:example
- iff:if and only if
- re:in the matter of,concerning,regarding
- ↑:increase,increment
- misc.:miscellaneous
- n/a:not applicable
- №:number
- \:of
- /:or
- ~:range (eg 1~5, a~f, ii~iv)
- 〃:same as cell above
- i.e.:that is,in other words
- ⇒:therefore,causing,resulting
- ※:which see,reference to
- w/:with
- w/i:within
- w/o:without
# Git
## Submit Pull Request
Open a pull request landing the finished [feature branch](#feature-branch) on `dev`.
#### Movement 1~7: Ready the Branch
Run [Ready for Feature Landing](#ready-for-feature-landing), its Movements 1~7 in order
#### Movement 8: Open the Pull Request
Push the branch if the remote lacks it, then run `gh pr create --base dev`, titled with the headline of the [feature branch summary](#feature-branch-summary) and bodied with its changes. Leave it unmerged for the reviewer, and reply with its URL, or the `gh` error.
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
## Ready for Feature Landing
Before merging the current [feature branch](#feature-branch), sync the docs it affects. Work in Movements; edit affected files in place and leave the rest untouched.
#### Movement 1~3: Sync Unit Test
If the project has unit tests, run [Sync Unit Test](#sync-unit-test) first.
##### {[Claude:Skill] Usage}
Invoke `sync-unit-test` skill via `Skill` tool.
##### {[Hermes:skill_view] Usage}
Load `sync-unit-test` skill with `skill_view`.
#### Movement 4: Learn the Feature Branch
Run [Discover Feature Branch](#discover-feature-branch), then use the change set it yields throughout Movement 5 & 6.
#### Movement 5: Record the Change Set in the CHANGELOG
Run [Maintain CHANGELOG](#maintain-changelog), recording the change set per [Repository CHANGELOG Writer](#repository-changelog-writer). The unreleased-only and deduplication rules come from that skill.
#### Movement 6: Sync AGENTS and CONTEXT
Run [Maintain Repository AGENTS](#maintain-repository-agents), updating any command, convention, or constraint the branch moved, per [Repository AGENTS Writer](#repository-agents-writer). Then update `CONTEXT.md` directly for any architecture the branch moved, per [Repository CONTEXT Writer](#repository-context-writer).
#### Movement 7: Commit the Work
Index the changes this work made, then run [Commit Sense](#commit-sense) to commit them.