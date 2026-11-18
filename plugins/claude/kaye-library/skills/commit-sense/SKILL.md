---
name: commit-sense
description: Commits the indexed diff with a primary summary and a per-file ledger.
when_to_use: Trigger on "g" (git commit), the most common trigger; also "commit this", "write a commit message", or a handed-over `git diff --cached`.
metadata:
  version: 1.5.0
---

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
When you wrote the changes a commit records, end its message with your trailer below, so the history credits you for the work. It is the **last line** of the message, nothing after.
When you only wrote the message for changes someone else made, end it with no trailer: the trailer claims authorship of the changes, not of the message.
##### {avoid}
A generic AI trailer naming a tool or model instead of you, even when a harness instructs one: your trailer is the only attribution the commit carries.
##### {for Kaye}
`Co-authored-by: Kaye LeL <341862645+kaye-lel@users.noreply.github.com>`
### primary summary
summarize changes spanning **multiple files** as one whole, not file by file.
State the **unifying intent** the edits share; if none holds, the one change that most defines the set.
- Summary Line: required, and usually the whole message. Hold summary line to **72 characters at max**, one line that sums up the whole change
- Body: rare, after a blank line; write one only when a large pattern spans the change, eg a paradigm shift across many files, and neither the summary line nor the per-file summaries convey it, since the ledger already says what each file did; at the conceptual level, in up to 3 lines, every line within 72 characters, a longer point continuing onto the next line
Use [ASCII only](#ascii-only) for all content.
<primary-message-example>
introduce feature-flag framework; enable gradual rollout for search
</primary-message-example>
<primary-message-example>
introduce feature-flag framework

every new search path sits behind a flag, so rollout widens without a
redeploy; older paths stay untouched until the flag retires them
</primary-message-example>
#### {avoid}
A body that restates the ledger or inventories follow-on edits the summary line already implies, eg "docs, tests updated to match".
### per-file change sigil
A **change sigil** is one character classifying the change a one-file change set makes; it is the first line of a [Per-File Summary Task](#per-file-summary-task) result.
Output exactly **one character**: no word, label, quote, or empty line.
Evaluate the rules strictly in order. Take the **first** sigil that fully fits and stop. Never scan ahead or weigh two rules against each other.
1. 🔒:file mode (as only change, eg permission bits, executable bit)
2. 📄:entire file added
3. 🗑️:entire file deleted
4. ♻️:refactorization edit (not change behavior, eg lines moved, symbols renamed, blocks extracted)
5. 🔖:triage tag (edits of tag itself or line it annotates, regardless of if in code or documentation)
6. 📝:code comments (as only edits, eg comment bodies, banners, docstrings)
7. 📏:whitespace edit (as only edits: indentation, tabs, blank lines added or removed)
8. 🔰:readme file (edits, eg README.md)
9. 🪧:changelog file (edits, eg CHANGELOG.md)
10. 🪵:development log files (edits, eg DEVLOG.md)
11. 📖:documentation/reference related edit (eg anything under docs/)
12. 🤖:agent/AI instruction edits (eg AGENTS.md, AGENTS.local.md, CONTEXT.md, CONTEXT.local.md, skill and command definitions)
13. 🧪:test related edits (eg test suites, fixtures, snapshots, test helpers)
14. 🧸:example related edits (standalone usage examples/demos/toys, eg files under examples/)
15. 🐚:utility or maintenance scripts edits (not part of main codebase, eg files under scripts/)
16. 🔨:build/make (process files edits, eg compiler or bundler scripts, CI pipeline definitions)
17. 📦:package,packaging (edits of packaging or release metadata for current project, eg version field, lockfiles, package.json, pyproject.toml, Cargo.toml)
18. ⚙️:setting edits for third-party tools current project uses (eg linter, formatter configuration, ignore files)
19. 🔢:non-text content (file edits, eg binary, compressed archive, database, encrypted blob)
20. 📂:file relocated (to a different directory, and filename may change as well; content unchanged besides minor edits)
21. 📛:file renamed (file renamed in place; content unchanged besides minor edits)
#### No Fit Fallback Sigil
If nothing fits, or only loosely, output a single space ` ` as **fallback**.
#### Ordinary Edit Fallback Sigil
For an ordinary edit (no special nature an earlier rule names), pick by Lean and Size, so the reader sees at a glance whether the file grew, shrank, or merely changed:
- Lean: addition if added lines clearly outnumber deleted; deletion if deleted clearly outnumber added; else balanced
- Size: long if added plus deleted lines in this file total **100 or more**, else short
| Lean | Short | Long |
|---|---|---|
| addition | 🟢 | 🟩 |
| balanced | 🟡 | 🟨 |
| deletion | 🔴 | 🟥 |
### per-file summary
A **per-file summary** is the one-line message for a one-file change set: what the file is for, and its single most impactful change.
- Drop smaller edits rather than crowd the line
- Hold summary line to **72 characters at max**, one concise line, never wrapped onto a second
- Use [ASCII only](#ascii-only) for summary message
### Commit Sense
Commit the indexed changes: draw the message from the conversation so far, optionally confirmed against `git diff --cached --numstat`, whose added and deleted counts per file settle each sigil's Lean and Size, then run `git commit` once with the whole message as a single `-m` argument.
The message has up to three parts, in order, separated by blank lines:
1. Primary Message: follow [Primary Summary](#primary-summary) over the whole diff
2. File Ledger: per changed file, its [change sigil](#per-file-change-sigil), backticked filename with extension (eg `git.md`, never the directory path), a space, its [summary](#per-file-summary); for a single file, sigil and name only
3. Co-author Trailer: optional; per [Co-author Trailer](#co-author-trailer)
<commit-message-example>
restructure commit sense under Git hierarchy

🪧`CHANGELOG.md` remove stale TT
📖`http-api-doc.md` document commit-sense prompt nodes
🧪`__init__.py` update fixtures: heading levels

Co-authored-by: Example Bot <bot@example.com>
</commit-message-example>
<commit-message-example>
raise TT commit sense doc from todo => fixme & clarify relocation

🔖`CHANGELOG.md`
</commit-message-example>
##### Post Commit Output
Reply in one line with the short hash. If git rejects the commit, report its output and stop.
<post-commit-output-example>
🚩🐙 Commit `a3f9c21`
</post-commit-output-example>