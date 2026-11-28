---
name: plan-for-suite
description: Splits oversized task into ordered, numbered Movements, then runs them under review — survey repository, write Plan file, hold for approval, execute 1 Movement per turn
when_to_use: 'On large, multi-file, multi-concern work wanted reviewable, not 1 pass. Triggers: plan this, break into Movements, go step by step. Start before any edit, so survey precedes Plan, Plan precedes 1st change. Not for 1-turn tasks'
metadata:
  version: 1.6.2
---

## Files & Folders
Files are assumed to be consistent between rounds. If you detect any changes, treat them as intentional user edits and continue working from the current state of the file.
----
When no specific naming format is required — for documents, resources, media, and other non-code files:
- respect a directory's existing naming convention for new entries within it
- otherwise, for a new file or folder:
  - Files: use [Kebab Case](#letter-case-kebab-case)
  - Folders: use [Pascal Case](#letter-case-pascal-case)
- if a file name must carry a date, the date leads it: `0YYYYMMDD` per [Date and Time Format](#date-and-time-format), then a hyphen, then the subject slug, eg `020260826-weekly-standup.md`. This sorts a directory chronologically on name alone
## Movement, Voice, and Suite
An explicit, multi-round user task runs as 3 nested units: Suite, Voice, and Movement. Never use them for simple, implicit, or single-round work.
**Suite**: the whole workflow for 1 such task
- holds 1+ Voices, the Main Voice always among them
- works on its feature branch, often 1 Suite = 1 feature branch, which every instrumental branch merges back into
- completes once every Voice has merged back and no Movement remains
**Voice**: 1 line of Movements within a Suite, run in order
- the **Main Voice** is the Suite's own line, marked 🧩: every Movement outside the other Voices, user Movements included; only the main session runs it
- every other Voice is an **instrumental Voice**, marked by its instrument emoji: agent only, with no user Movement, approval, or question inside it
- every Voice must be able to run in parallel with the rest, never waiting on another Voice's unmerged work
- each instrumental Voice works on its own instrumental branch and linked worktree, cut from the feature branch and merged back into it once its Movements are done
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
- voice (line of Movements within a Suite; any but the Main Voice is an instrumental Voice: agent only, soloed by a subagent or run in its own session, in parallel on its instrumental branch, then merged back into the feature branch)
- suite (unit contains 1+ Voices)
in general: Round < Movement < Voice < Suite
### {[git] Usage}
Commit each Movement's edits as exactly one git commit: 1 Movement = 1 commit.
Often 1 Suite = 1 feature branch. 1 Voice = 1 instrumental branch, cut from the feature branch and merged back into it.
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
# Style Guide
### Diagrams
Use **Mermaid** syntax inside fenced code blocks to render diagrams, graphs, flowcharts, and visual representations. Eg
```mermaid
graph LR
  A --> B --> C
```
Read "Y vs X" as Y on the y axis, X on the x axis, eg "Height vs Time".
## Letter Case
### Letter Case Kebab Case
lowercase words joined by hyphens, eg: `total-price`
### Letter Case Pascal Case
each word capitalized, no separators, eg: `TotalPrice`
## Date and Time Format
### Year Month Day Format
Write `0YYYY-MM-DD`, the year padded to five digits. The day of week code prefix is optional.
`H 02015-01-15`, `02015-01-15`, `A 01984-12-31`
### (element-dt-days-of-week)
Each code is one letter, unique per day, because English initials repeat (T and S each name 2 days); German fills the gaps. Day of week codes:
- A:Monday (1st letter, 1st workday)
- D:Tuesday (in Dienstag)
- E:Wednesday
- H:Thursday
- R:Friday
- S:Saturday
- U:Sunday
# Git
## Tend Linked Worktree
Give each task, often a plan or suite, one linked worktree on its single branch, so the main worktree stays untouched. The branch may be of any kind: a [feature branch](#feature-branch), an instrumental branch, a hotfix or release branch, ~.
Never share a linked worktree across tasks or switch its branch, nor split a plan or suite per Movement. The 1 split allowed: each instrumental Voice of a Suite gets its own linked worktree on its instrumental branch, whatever its mode.
A linked worktree sits inside the repository's workspace folder, named `REPO-WT-BRANCH`:
```text
WS-kaye-library/
├── kaye-library/                                # main worktree, on dev
├── kaye-library-WT-add-search-filter/           # linked worktree, on add-search-filter
└── kaye-library-WT-add-search-filter-violin/    # linked worktree, on instrumental branch add-search-filter-violin
```
- `WS-`: prefix of a workspace folder, which holds several worktrees
- `-WT-`: infix marking a linked worktree
### Plant the Linked Worktree
Plant the task's linked worktree as `REPO-WT-BRANCH` in the workspace folder, linked to the task's existing branch. If none exists, create the branch with the worktree, from the branch it will merge back into: the integration branch for a feature branch, the feature branch for an instrumental branch.
### Uproot the Linked Worktree
Once the task is done, uproot its linked worktree, but only after every edit it holds is committed and merged into the branch it merges back into: the main worktree's branch for a feature branch, the feature branch for an instrumental branch. If any edit is not, stop and report.
## Prune Merged Branches
You delete **local** branches already merged into the current branch. Nothing else is in scope — no remote or remote-tracking refs, tags, stashes, worktrees, index, or working tree. Stop and say so if `HEAD` is detached or a merge, rebase, cherry-pick, or bisect is in progress.
#### Candidates
- take the set from `git branch --merged`, resolved against the current branch
- drop the current branch, protected branches (`main`, `master`, `develop`, `trunk`, `release/*`), and anything the user names
- a branch absent from that set is never a candidate, for any reason
#### Delete
`git branch -d` only. `-D` and `--delete --force` are forbidden, including as a retry; a refusal from `-d` stands — leave the branch and report it.
Present candidates and exclusions together and wait for an answer whenever the set is unclear: an unstated protected list, a candidate that looks like live work, or a current branch that is not the integration target. Deleting nothing is the correct outcome of an unanswered question. Once settled, pass every remaining name to a **single** `git branch -d` call — never loop, never one at a time.
#### Report
- each branch deleted, with the tip hash Git prints, so the user can recover it
- each branch skipped, and why
- if nothing qualified, say so in one line and stop
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
## Perform Feature Landing
Land the current [feature branch](#feature-branch) on `dev`: ready it, then merge it, so `dev` never receives stale docs.
#### Movement 1~7: Ready the Feature Branch
Run [Ready for Feature Landing](#ready-for-feature-landing) whole. Continue only once its commit lands; keep its [feature branch summary](#feature-branch-summary) for Movement 8.
#### Movement 8: Merge into Dev
Merge per [Commit Sense For Branch Merging](#commit-sense-for-branch-merging) (feature into dev). When you work in a linked worktree, do every step in the main worktree, since it holds `dev`.
1. `git switch dev`, then `git merge --no-ff --no-commit FEATURE`: a merge commit records the landing, and the pause lets you word it
2. on conflicts, run [Resolve Merge Conflict](#resolve-merge-conflict), then go on
3. write the message, Git's drafted one read from `git rev-parse --git-path MERGE_MSG`, then `git commit` once
Stop at the merge commit: push and branch deletion wait for the approval of Movement 9.
#### Movement 9~10: Scrub After the Landing
Run [Scrub After Feature Landing](#scrub-after-feature-landing) whole, once the merge commit lands. If any earlier Movement halts, report where and why in one line, then stop.
## Plan for Suite
This uses the [Movement, Voice, and Suite](#movement-voice-and-suite) concepts on a Plan file — a Plan is a Suite, so it holds multiple Movements.
Two *Bars*, then Execution:
### Bar 1: Gather
Do **not** start editing. Read before you plan.
Resolve the task's scope from the repository itself — entry points, existing conventions, the files the task will touch, and anything the description leaves ambiguous. Prefer reading the actual code over assuming its shape.
Establish where the project stands **now**: what already exists, what is partially done, what is missing. The Plan starts from the real state, never from a clean slate.
Where the reading leaves intent unclear — scope, priorities, trade-offs, which of several readings is meant — ask the user rather than deciding yourself.
### Bar 2: Write the Plan
The Plan divides the task into Movements.
The Plan is a **deliverable** and lives in a **Plan file**, so later Movements can revise it in place.
Lay the file out per [Plan File](#plan-file).
Hand the Plan to the user and **stop**. The codebase stays exactly as it is until they approve.
##### Movement Record
The Plan must be **readable at a glance** and **workable in order**. Any layout serving both is fine. Record for each Movement:
- Scope: the files it touches, all named, and few
- Statement: what changes and why, in a line or two — never a code dump
- **End State**: what *Working* means once the Movement closes, so review can stop there
- Party (who performs it): you, the user, or another party by name; give the user what lies beyond your reach, eg a GUI step, a login, a device, an approval
- Status: always write `Pending` when first writing the Plan
Record no Order field. With only the Main Voice, the Movement numbers give the order; with instrumental Voices, `## Order` holds every dependency.
##### Voice Split
Deciding how many Voices to run is a balance: more Voices means more parallel work, so the Suite finishes sooner.
- Default to more Voices: split the work into as many parallel Voices as its dependencies allow
- Do not split too fine: every Voice holds at least 5 Movements; below that, combine its tasks into another Voice
- When both pull against each other, take the most Voices that still keep every Voice at 5 or more Movements
#### Plan File
- Name: [Kebab Case](#letter-case-kebab-case) slug of the task, ending `-suite-plan.md`, eg `auth-refactor-suite-plan.md`
- Location: first available of workspace root, repository root, your own temporary location
- 1 Plan file holds the whole Suite, every Voice included
Open the file with the preface below, *verbatim* and ahead of all Plan content, so whoever executes it reads the terms before the first Movement.
<plan-for-suite-preface>
Before working from this file, invoke the skill for the Voice you run: `play-suite` if you run the Main Voice, `solo-voice` if you run an instrumental Voice.

If you run the Main Voice, ask the user whether to run under `cascade-all-movements` or `halt-each-movement`, then follow the chosen skill.
</plan-for-suite-preface>
Top-level headings, all `##`, in this order after the preface:
- `## Context`: what a reader needs to grasp the Plan at a glance, high level, as an indented outline: the goal, the state it starts from, each [Housekeeping Movements](#housekeeping-movements) decision that came out yes with a one-line reason (the feature branch with its name, the linked worktree with its path, each instrumental Voice with its instrumental branch name)
- `## Terrain`: what belongs to this Plan alone, in detail: technical particulars, where to find the relevant files, constraints, anything a Movement leans on
- `## Design`: optional, only when the Plan brings a complicated new design, eg an API or a data shape; where the design replaces something, compare new against old side by side
- `## Order`: optional, only with instrumental Voices: a Mermaid graph of every Movement's dependencies, each instrumental Voice a subgraph, per [Diagrams](#diagrams); it holds every dependency, so the Movement record carries no Order field
- `## Rework`: optional, absent from a first draft; the history of every [rework](#plan-for-suite-rework), oldest first: append 1 numbered entry per rework, never edit or drop an earlier one, even when a later rework reverses it; each entry holds the finding (the Plan's assumption, the reality, the cost) and the Movements it revised, removed, added, or split
- `## Main Voice`: the Main Voice's Movements
- `## 🎻 Violin Voice`: 1 per instrumental Voice, in instrument order, each holding its Movements
###### Movement Heading
In the Plan file, head each Movement `🧩a: Title` in the Main Voice and `🎻a: Title` in an instrumental Voice, with its Voice's own emoji, as an `h3` under its Voice's `h2`. Between number and colon, add, in order and only when they apply:
- `{party}`: for a Movement that is not yours, never for your own
- `[workspace]`: when the task spans several workspaces or repositories
The user is a party too, by their own name, eg `{John}`.
```
### 🧩5 [api]: Wire Up the Config Loader
### 🧩6 {John} [api]: Approve the Staging Deploy
### 🎻2 [api]: Add the Retry Wrapper
```
##### {[git] Usage}
Never index or commit the [Plan File](#plan-file), unless the user explicitly asks: it is run scratch, not project history.
#### Housekeeping Movements
Housekeeping Movements set up and tear down the Suite's branches and worktrees: cutting, planting, merging, uprooting, pushing. Write one only if the Suite needs it, as an ordinary Movement of the Main Voice, decided from the repository state gathered in Bar 1, without asking; a Suite that needs none gets none.
###### Opening Movement
If the Suite needs a [feature branch](#feature-branch), open with a Movement that cuts it. It is needed when the repository uses git, the Suite's commits should land together, and some Movement edits a tracked file; it is not needed when the user said to work on the current branch.
If the main worktree is busy, or the user asked to leave it untouched, that Movement also plants the linked worktree per [Plant the Linked Worktree](#plant-the-linked-worktree), which cuts the feature branch when missing.
###### Closing Movement
If the Suite has a feature branch, close with a Movement that lands it per [Perform Feature Landing](#perform-feature-landing), then scrubs up per [Scrub After Feature Landing](#scrub-after-feature-landing).
If stale merged branches are in the way, add 1 Movement that prunes them per [Prune Merged Branches](#prune-merged-branches).
###### Instrumental Voice Movements
Form an instrumental [Voice](#movement-voice-and-suite) only if the Suite has a feature branch and a stretch of 3+ Movements you perform alone whose Scopes share no file with the Main Voice or any other Voice. Otherwise keep the work in the Main Voice; favor the Main Voice and keep the Voice count low.
Each Voice formed adds 2 housekeeping Movements:
- opening, in the instrumental Voice: plant its linked worktree per [Plant the Linked Worktree](#plant-the-linked-worktree), cutting its instrumental branch from the feature branch
- closing, in the Main Voice: after the Voice's report, merge its instrumental branch into the feature branch, uproot its linked worktree per [Uproot the Linked Worktree](#uproot-the-linked-worktree), and prune the merged branch per [Prune Merged Branches](#prune-merged-branches); place any Movement that depends on the Voice after it, and record the dependency in `## Order`
### Plan for Suite: Execution
Starts only after the user approves the Plan. Follow Plan order — nothing skipped, nothing combined.
The Plan file holds the context and Terrain: start from it, read your Movements there, and explore the repository only when a Movement needs more. Leave the Plan file untouched unless a rule says to write it.
Never work around a mismatch with the Plan, an End State that will not hold, or anything a Movement cannot settle alone.
Each Voice works only on its own branch and in its own worktree, and never touches another Voice's.
Housekeeping splits by Voice: the instrumental Voice cuts its instrumental branch and plants its linked worktree, as its own opening Movement; the Main Voice merges, uproots, and prunes, as its own closing Movement. Any other housekeeping Movement is an ordinary Movement.
Each Movement runs these steps in order:
1. Movement In: enter the Movement next in order
2. Task: do its work, touching nothing outside the Movement's boundary, until its End State holds
#### {[git] Usage}
1 Movement = 1 commit. A Movement that edits no workspace file, such as a user Movement, commits nothing.
### Play Suite
You play the Main Voice of an approved Plan.
If not already answered, ask whether the Main Voice runs under `cascade-all-movements` or `halt-each-movement`.
Run each Movement's steps per [Plan for Suite: Execution](#plan-for-suite-execution), then close it:
3. [Movement Recap](#movement-recap)
4. Movement Out: return control to user
On resume, Movement In to the Movement its Status names, per [Saved State](#saved-state).
Check the Movement's Party at Movement In. Your own Movements run as above; any other party follows [Movement Parties in Execution](#movement-parties-in-execution).
Movement order binds your judgement, not the user's. Out of sequence, several at once, one skipped, the Plan set aside — obey without protest, noting which Movements are left.
##### Instrumental Voices
Start each instrumental Voice once every Movement it depends on is done:
1. choose its mode: a subagent by default, wherever a subagent tool exists; its own session when the Voice outgrows a subagent's budget, when the user wants to watch it, or when no subagent tool exists
2. start it with 1 prompt naming the Plan file and the Voice, and nothing else: the Voice reads the Plan and starts on its own with `solo-voice`; in session mode, ask the user to open a new session and give it that prompt
3. go on with the Main Voice on the feature branch; a Main Voice Movement that depends on the Voice waits for its closing Movement
On the Voice's report:
- every End State met: run the Voice's closing Movement, merging its instrumental branch into the feature branch, uprooting its linked worktree, and pruning the merged branch, then mark the merge back with 🎌 in the Movement Recap
- a stop or a mismatch: halt per [Plan for Suite: Rework](#plan-for-suite-rework)
##### Saved State
The Plan file doubles as the run's saved state, so a run survives the end of a session:
- Pause: only when the user explicitly states "pause", never on a halt; then set each Movement's Status keyword to where the run stands
- Resume: read each Movement's Status, Movement In to the earliest not `Done` or `Dropped`; check that the feature branch, each open instrumental branch, and their linked worktrees still exist; on a mismatch with the workspace, halt per [Plan for Suite: Rework](#plan-for-suite-rework)
Status keywords, written only on a pause or a rework. Each Movement carries exactly one keyword at any moment:
- `Pending`: not entered yet, the starting keyword
- `Done`: closed Working
- `Halted`: stopped, awaiting rework
- `Dropped`: removed by rework
##### Movement Parties in Execution
For a user Movement, never do the work yourself. Guide interactively:
1. Movement In: say the Movement is theirs and its goal
2. give one step at a time; wait for their report before the next
3. halt per [Plan for Suite: Rework](#plan-for-suite-rework) if a report contradicts the Plan
4. settle the End State by their confirmation or your check, and say which
5. Movement Out once it holds
For another party, hand over steps and End State, await its report, then verify.
#### Movement Recap
Always end the Turn with a 2-line [Turn Progress Dispatch](#turn-progress-dispatch), each line prefixed per [Movement Notation](#movement-notation) and [Dispatch Marks](#dispatch-marks):
```
🎏 🧩3\7 Rewrote the Entry Point
🧭 🧩4 Wire Up the Config Loader
```
At an instrumental Voice's merge back, add its line:
```
🎌 Violin Test Fixtures Merged Back
```
Except when the entire Plan is completed — then end with a 1-line Turn Progress Dispatch naming the Plan instead:
```
🏁 Auth Refactor
```
#### {[agent] Fallback}
With no subagent tool, run every instrumental Voice in session mode.
### Plan for Suite: Rework
Halt the moment reality stops matching the Plan — a bug, a false assumption, a wrong or unnecessary Movement, unaccounted-for work, a user redirect, anything unanticipated. Never work around it.
1. present the finding: the Plan's assumption, the reality, and the cost to the Movements still ahead
2. rewrite the Plan whole — edit it in place, or author an entirely new file — never a diff, excerpt, or the rework alone. Keep completed Movements untouched and numbered; revise, remove, or add the rest as the finding demands, and append the rework to the history in `## Rework`
3. set every Movement's Status keyword per [Bar 2: Write the Plan](#bar-2-write-the-plan), so the file reads cold as exactly how far the run got and what the finding cost
4. never renumber to make room. A split Movement keeps its number and gains sub-Movements beneath it — `Movement 1` becomes `Movement 1.1` and `Movement 1.2`
5. present the revised Plan and hold for approval, as in [Bar 2: Write the Plan](#bar-2-write-the-plan)
6. once approved, Movement In to the earliest unfinished Movement, and not sooner