---
name: maintain-repo-docs
description: Updates existing repository `docs/` files against what changed, editing in place
when_to_use: 'Triggers: "update the docs", "docs still show the old command", renamed file, removed feature, changed command'
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
# Style Guide
## Letter Case
### Letter Case Kebab Case
lowercase words joined by hyphens, eg: `total-price`
### Letter Case Pascal Case
each word capitalized, no separators, eg: `TotalPrice`
## Style Guide Good Writing
- Correct spelling, grammar, punctuation, sentence structure, and verb tense errors.
- Preserve the original meaning, voice, tone, style, word order, and vocabulary as much as possible unless the user requests heavier rewriting.
- Make only the minimum changes needed to improve correctness, readability, and clarity.
- Ensure the revised text is clear, polite, and free of language errors.
- Use American English by default, but if the original text clearly uses another spelling convention, preserve that convention.
- Expand uncommon abbreviations only when doing so improves clarity.
- Do not add new information, remove intended information, or change the substantive meaning of the text.
- Avoid generic filler when details are unavailable
- Avoid dense prose, generic filler, and unnecessary complexity
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
## Secondary Language Marking
Put a key word in a secondary language in `[]`, right after its primary-language counterpart, no space between.
`请检查配置文件[config file]中的路径[path]是否正确。`
## doc writer
Apply these rules to the topic documents under `docs/`, formatting them per [Style Guide Markdown Format](#style-guide-markdown-format) and writing them per [Style Guide Good Writing](#style-guide-good-writing).
A single document focuses on one very specific topic, or one system with a clear boundary.
### Repository Doc Writer
Draw from the repository's code and configurations, and verify every example against the source. Link every file written here from `README.md`, per [Documentation Links](#documentation-links).
### Maintain Repository Docs
You work from a **change set**: what the conversation and the repository have altered since the docs were written. A document the change set never reaches is left exactly as it reads.
1. edit in place: update what the change set moved, fix references it broke, cut what it made stale, duplicated, or unsupported
2. leave each document's audience, scope, and sound wording alone
3. verify links, paths, commands, and examples against the codebase
4. create a document only where the change set requires it
5. follow [Repository Doc Writer](#repository-doc-writer), [Style Guide Markdown Format](#style-guide-markdown-format), and [Style Guide Good Writing](#style-guide-good-writing), then return a brief summary listing changed files