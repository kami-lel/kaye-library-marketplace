---
name: agent-files-and-folders
description: 'Governs files & folders an agent touches: treats between-round changes as intentional user edits, names new non-code files in Kebab Case, folders in Pascal Case, dated names led by `0YYYYMMDD`'
when_to_use: 'Creating, naming, or renaming a document, resource, media file, or folder, or meeting a file changed since last round: "new file", "what to call this", "name the folder", dated notes or reports. Not for code identifiers or a project''s fixed file names, eg `README.md`'
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