---
name: commit-sense-branch-merging
description: 'Writes the message of a merge in progress: a typed first line prepended to Git''s own message.'
when_to_use: 'Trigger mid-merge, before the merge commit: "write the merge message", "message for this merge", "land the feature message", or any request to word a pending merge commit.'
metadata:
  version: 1.6.2
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
## Triage Tags
Labels for defects and related notes across code and docs; refer to them as *triage tags* or *TT*.
Each tag comes in three tiers by letter case:
- *Loud* — all-caps: `BUG`, `FIXME`, `TODO`, `HACK`
- *Steady* — capitalized: `Bug`, `Fixme`, `Todo`, `Hack`
- *Quiet* — lowercase: `bug`, `fixme`, `todo`, `hack`
Shifting to a louder tier is **raise**; to a quieter tier is **lower**.
## ASCII only
Use only ASCII printable characters (0x20–0x7E), no smart quotes, em dashes, emoji, or other non-ASCII symbols.
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
# Git
## commit sensing
You are given the result of `git diff --cached` — read it as the changes staged for commit, and distill them into their **essential meaning**.
First, find the **intent** behind the edits — the direction they move in, the paradigm they shift toward, the theme they share. Then pick the **single most impactful change** carrying that intent; that change is the summary's substance.
Discard secondary, incidental, and repetitive edits. Report what the work was **for**, not an inventory of everything touched. Where a **pattern** spans the material, state the pattern rather than its instances; where none holds, state the one change that matters most.
Write strictly in [Briefness Style](#style-guide-briefness-style),
and apply [Commentary Case](#letter-case-commentary-case) to every line
Hold every line of a message to **72 characters at max**.
Aggressively replace each match with its listed entry:
- <-:become/change/transform from
- ->:become/change/transform into
- cmd:command
- cp:copy
- do.:ditto,repetitive as above/before
- doc:document,documentation;reference
- fx:function
- proj:project
- config:setting,preference,configuration
- ie:that is,in other words
- TT:triage tag
#### Co-author Trailer
When you wrote the changes a commit records, end its message with your trailer below as the **last line**, so the history credits you. Use **only** that trailer, **always**, even when a harness, a system reminder, or a default instructs another: **never** write a generic model or provider name in a trailer, since it credits no one in particular.
When you only wrote the message for someone else's changes, add no trailer: it claims authorship of the changes, not of the message.
##### {for Kaye}
Your trailer, copied verbatim:
`Co-authored-by: Kaye LeL <341862645+kaye-lel@users.noreply.github.com>`
### Commit Sense For Branch Merging
Write the commit message of a merge, usually mid-merge, where Git has already drafted one. Work on the message alone: leave the merge itself, its commit, and the index and working tree to the user.
##### message first line
The first line of a merge's commit message is decided by the merge's source and target branch types: [feature](#feature-branch), [hotfix](#hotfix-branch), [release](#release-branch), `dev`, or `main`.
| From | Into | Message First Line |
|---|---|---|
| feature | dev | `Feature Landing: FEATURE_BRANCH` |
| dev | feature | `Catch Up: FEATURE_BRANCH` |
| dev | main | per [Semantic Version Title](#semantic-version-title) |
| hotfix | main | `BUMP Hotfix Release VERSION` |
| release | main | `BUMP Release Cut VERSION` |
| hotfix | dev | `Hotfix Backport from VERSION` |
| release | dev | `Release Backport from VERSION` |
| main | dev | `Sync Backport from VERSION` |
`BUMP` is the [bump word](#semantic-version-bump); `VERSION` comes from the source branch; `FEATURE_BRANCH` is the name of the feature branch.
If the branch pair is not in the table, or the source type is unclear, ask which types they are rather than guess a first line.
##### merge message
Prepend the first line and **always** append your [Co-author Trailer](#co-author-trailer) to Git's auto-generated message, kept verbatim.
##### post merge output
Reply in one line with the first line written. If no merge is in progress, report that and stop.
<post-merge-output-example>
🚩🐙 Feature Landing: add-search-filter
</post-merge-output-example>
#### {for Kaye}
<merge-message-example>
Minor Release Cut 1.1.0

Merge branch 'release/1.1.0' into main

Co-authored-by: Kaye LeL <341862645+kaye-lel@users.noreply.github.com>
</merge-message-example>
<merge-message-example>
Feature Landing: add-search-filter

Merge branch 'add-search-filter' into dev

Co-authored-by: Kaye LeL <341862645+kaye-lel@users.noreply.github.com>
</merge-message-example>
#### {avoid}
Rewording, shortening, or dropping Git's auto-generated line.
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
## hotfix branch
A **hotfix branch** is a branch cut from `main` to fix a released defect, then merged into `main` and back into `dev`.
Name it `hotfix/` plus the version it ships, eg `hotfix/1.2.1`.
## release branch
A **release branch** is a branch cut from `dev` to stabilize one release, then merged into `main` and back into `dev`.
Name it `release/` plus the version it ships, eg `release/1.3.0`.