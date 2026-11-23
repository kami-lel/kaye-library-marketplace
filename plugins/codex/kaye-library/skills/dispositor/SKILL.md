---
name: dispositor
description: Writes & maintains structured, hierarchical personal notes under 1 consistent filename, framing & prose grammar.
when_to_use: 'Trigger on any request to draft, continue, reformat or audit a personal note file — reading notes, lecture notes, session notes, journals. Keywords: note, filename, dated heading, shorthand.'
metadata:
  version: 1.6.0
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
### Header Separation
You must add *empty lines* before each section header, with the **number of empty lines determined by the header level** provided in the table.
Note: Do not include the text inside parentheses `()`, these are *instructions* showing where to insert empty lines.
#### Long File
| Level | MD Header                       | Empty Line Before |
|-------|---------------------------------|-------------------|
| 2     | `## Level 2 Header Example`     | 34                |
| 3     | `### Level 3 Header Example`    | 13                |
| 4     | `#### Level 4 Header Example`   | 5                 |
| 5     | `##### Level 5 Header Example`  | 3                 |
| 6     | `###### Level 6 Header Example` | 2                 |
    <header-separation-long-file-example>
    (...)
    Brief project description.
    (34 EMPTY LINES BEFORE LEVEL 2 HEADER)
    ### Installation
    Step-by-step instructions.
    (13 EMPTY LINES BEFORE LEVEL 3 HEADER)
    #### Usage
    (...)
    </header-separation-long-file-example>
#### Medium File
| Level | MD Header                       | Empty Line Before |
|-------|---------------------------------|-------------------|
| 2     | `## Level 2 Header Example`     | 13                |
| 3     | `### Level 3 Header Example`    | 5                 |
| 4     | `#### Level 4 Header Example`   | 3                 |
| 5     | `##### Level 5 Header Example`  | 2                 |
| 6     | `###### Level 6 Header Example` | 1                 |
    <header-separation-medium-file-example>
    (...)
    Brief project description.
    (13 EMPTY LINES BEFORE LEVEL 2 HEADER)
    ### Installation
    Step-by-step instructions.
    (5 EMPTY LINES BEFORE LEVEL 3 HEADER)
    #### Usage
    (...)
    </header-separation-medium-file-example>
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
## Dispositor
you maintain structured, hierarchical notes taken from **source material** — the thing the note is a note *of*, whether a text, a screen, a sitting or a recording. The source material is the authority: the note's heading tree follows the source's own divisions, its wording follows the source's own wording, & every unbracketed line traces back to something the source actually held. 1 grammar governs filenames, framing, prose density & content arrangement, so any note in the corpus reads the same way regardless of which source material produced it.
#### File Naming
- Filename Is an ID, Title Is a Description: the slug identifies the file — short, stable, machine-sortable; the `#` title describes its content — longer, natural-language, free to carry punctuation & the source's own wording
- The 2 Need Not Match: expect `read-note-agent-design.md` to open on `# Designing a Reading-Note Agent` — divergence is normal, never a defect to repair
- Slug Outranks Title on Identity: on disagreement over subject, date or scope, trust the slug — titles get carried over from an earlier session & left unsynced
#### Structure Follows the Source
- Headings Mirror the Source's Divisions: 1 heading per division the source itself makes, named & ordered as the source names & orders them ⇒ the file's heading tree is the source's tree, not an authored taxonomy
- Every Division Listed, Covered or Not: stub a division the source skipped, deferred or left untouched rather than dropping it ⇒ the heading list doubles as a completeness record of the whole source
- Local Heading for a Local Section: a one-off sub-case inside a division takes a [Local Heading](#markdown-heading-format), read against that division alone, rather than a rung on the file's main tree
- Note Language Follows Source Language: write in whatever language the source uses, even against the corpus's dominant language — a note transcribes, never translates
#### Bracketed Lines Sit Outside the Source
`[]` marks a line w/o a counterpart in the source material: the user's own annotation, a question raised while reading, a cross-link, a doubt, a reminder to return.
- Everything Unbracketed Maps 1:1: a plain line answers to something the source held — a paragraph, a control, an agenda item
- `[]` Answers to Nothing in the Source: it is neither source content nor a note or summary of source content, & carries no claim about what the source said
- Strip-Clean Test: deleting every `[]` line leaves a note still readable as a faithful record of the source, w/ no gap where the brackets stood
- Bracket Sits at Its Subject's Level: place the line in the structure beside the material it comments on, nested exactly as a source line there would be
<bracketed-line-example>
- Comparative advantage: gains from trade hold even w/ absolute advantage on both goods
- [does this survive transport cost? check Ch.7]
</bracketed-line-example>
#### Prose & Shorthand
- Private Shorthand, Never Reader-Facing Prose: write body text in the user's decode-only abbreviation scheme, articles & helper verbs dropped, tuned for the author's own re-reading speed
- Fragments Over Sentences: prefer noun-phrase fragments, arrow & colon shorthand
- Terse Comparative Framing: mark contrast w/ the scheme's comparison abbreviation, not a spelled-out sentence
- Comments Echo Prose Terms: word in-block comments w/ the exact surrounding vocabulary ⇒ code & explanation stay 1 vocabulary
#### Content Practice
- Pair Formal w/ Informal: place the plain-language gloss & the formal statement back to back when a concept carries both
- Cross-Reference Over Repetition: point at the section already holding a value instead of restating it
- Worked Example Under Its Category List: follow abstract categories w/ a concrete labeled example reusing the identical labels