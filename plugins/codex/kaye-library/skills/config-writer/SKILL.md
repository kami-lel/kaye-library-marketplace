---
name: config-writer
description: Writes & maintains structured, hierarchical personal notes, specializing in capturing an app's, game's or system's preferences, settings & config state as a reproducible snapshot.
when_to_use: 'Trigger on any request to record, update or review a settings, preferences, keybind or config snapshot for an app, game or OS. Keywords: settings, preferences, config, keybind, build/version.'
metadata:
  version: 1.6.1
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
### Config Writer
settings specialization: transcribe an app's or program's config/option/setting into a reproducible note. Source material here is the program's live settings surface — its controls & displayed values, read as shown — & its divisions are that surface's pages & tabs.
Write per [Style Guide Briefness Style](#style-guide-briefness-style). Aggressively also use the following shorthand in place of its full form, wherever unambiguous:
- ∅:not applicable
- ◎:selected (bullseye)
- ●:selected (filled circle)
- ☑:selected (checkbox with a tick)
- ☒:selected (checkbox with a cross)
- ⁇:unknown
- ❓:unknown
- ○:unselected (empty circle)
- ☐:unselected (empty checkbox)
##### Metadata
- File Title: the app/program's normal name + configs/options/settings, eg `Adobe Acrobat Pro settings`
- Program Name & Build (optional): directly under the File Title, state the exact program name & build/version the note applies to, kept simple, eg `Adobe Acrobat Pro DC 2023.003.20201 (x64)`
- Filename: the File Title slugged, eg `adobe-acrobat-pro-config.md`
##### File Structure
- Group Parent Line Carries No Value: a control group nests as a sub-list under `- Heading Name:` — colon, then nothing, no value & no trailing glyph
- Sub-App Sections Nest Under Their Route: keep a separately-windowed feature under the path reaching it, w/ a 1-line prose note on how to get there
- Local Sub-Case Is a Collapsed Panel or Rare Sub-Mode: what takes a [Local Heading](#markdown-heading-format) inside a page is a panel or mode the page hides behind a control, never a plain group of entries
##### Entry & State
**Recording deviation from default is the point of the note.** An untouched entry stays flat; a changed entry always carries its default alongside its current value.
- Field Name, Then Whitespace, Then Value: every entry — toggle and select-one included — is written in that fixed order, `Field Name:` first, padding spaces second, `value` last; no entry uses a leading glyph in place of the colon
- Padding Aligns the Level: within 1 page/tab (or 1 nested group), the padding whitespace after each `Field Name:` is sized so every entry's value starts in the same column — a level's entries read as an aligned column, not a ragged list
- Deviation Anchors at the Desired Value: a changed entry reads `desired value` ← `default value`, no bold; the alignment column is set by where `desired value` starts, w/ the default trailing after, left-aligned to that same column across the level
Entry Types — the value each places after the colon:
- On/Off Toggle: `☑` or `☐`
- Select-One: the chosen glyph alone, eg `●` — unchosen options are not shown
- Input Field: a typed, free-text value, quoted — enclosed in `` `content` ``
- Dropdown / Numeric Field: the chosen option's name or a plain number, unquoted
- Greyed Out / Unavailable: `∅`
- Unknown: `??`
- Button / Clickable Action: no colon, no value — the whole line is the verb action alone, italicized, eg *Launch Benchmark*
A glyph value may carry a simple label, eg `☑ On`, `● Fast`; the label is optional, but on a deviation it pairs on both sides or on neither.
Naming:
- Long Entry Name Compresses with `~~`: an entry name that runs to a full sentence keeps only its first 3 words + last 1 word, joined by `~~`, eg, for "Automatically download and install updates when a new version becomes available"
- Name Non-GUI Setters Explicitly: call out an environment variable or equivalent as the atypical, more powerful route to the same value
Structure:
- Procedures Sit Beside State: embed how-to-configure steps at the same level as flat entries when a setting needs non-trivial action to change
- Module Sets Stay 1 Flat List: track independent plugins, watchers & modules as a single checkbox list under 1 heading, never a heading each
##### Example
```
- Show Toolbar:                             ☑
- Show Splash Screen:                       ☒ ← ☐
- Startup Behavior:                         ● Show start screen ← ○ Reopen last file
- Default Save Format:                      PDF/A ← PDF
- Recent Files Count:                       10
- Hardware Acceleration:                    ∅
- Automatically download and ~~ available:  ☑
- *Launch Benchmark*
- Advanced:

  - Default Save Location:  `~/Documents/Acrobat` ← `~/Documents`
  - Cache Size (MB):        512 ← 256
  - Log Level:              Debug ← Info
```
#### Keybinding Writer
Aggressively replace keys with shorthand:
- 🖰:mouse,mouse movement
- ⌘:control/command
- ⌥:alt/option
- ⇧:shift
- ⎋:escape
- ⇥:tab
- ⇪:caps lock
- ␣:space
- ⏎:return/enter
- ⌫:backspace
- ⌦:delete
- ⇟:page down
- ⇞:page up
- ⇱:home
- ⇲:end
- ⮝:up arrow
- ⮞:right arrow
- ⮜:left arrow
- ⮟:down arrow
Chord modifier order: ⌘⌥⇧, eg ⌘⇧F
Modifier may take L or R prefix, eg L⇧
----
Mouse buttons:
- ◖:left click
- ◗:right click
- ◉:wheel, middle click
- ④:mouse button 4
- ⑤:mouse button 5
Wheel ◉ + modifier: ⇧ up, ⇩ down, ⇳ either direction. Eg ◉⇧
----
Controller buttons:
- Ⓐ:a button
- Ⓑ:b button
- Ⓧ:x button
- Ⓨ:y button
- 🄻:left bumper
- 🅁:right bumper
- 🅻:left trigger
- 🆁:right trigger
- Ⓛ:left stick
- Ⓡ:right stick
- ✚:d-pad
- ▲:d-pad up
- ▶:d-pad right
- ◀:d-pad left
- ▼:d-pad down
- ⧉:view button
- ☰:menu button
Stick Ⓛ Ⓡ + modifier: ⤓ press, ⇦ ⇧ ⇨ ⇩ push.
Eg Ⓛ⤓ left stick press
Stick either direction: ⇧Ⓛ⇩ vertical, ⇦Ⓛ⇨ horizontal