---
name: hunt-job-opportunity
description: Gathers job opportunity information from any available source and formats it into briefs, one per job, each with a title-and-company heading, key details, and a briefness-style overview.
when_to_use: Trigger on "job hunt," "find me a job," "what job opportunities are there," or any ask to gather and present job openings, including openings already mentioned in this conversation. Not for revising a single job posting or listing calendar events.
metadata:
  version: 1.6.2
---

## Task Blockage Workaround
A task is **blocked** when you need information you cannot obtain, eg network down, connection refused, permission denied.
When a task is blocked:
1. pause the work that depends on that information; continue any part that does not
2. ask the user for it, in the reply format below
3. once the user provides it, resume where you paused and finish the task
#### Reply Format
Each line carries exactly one emoji: 🚧 lines name what is blocking, one line per item; the closing 🙋 line asks for what clears the first 🚧 line.
One item:
```markdown
🚧 Network Down, Cannot Fetch the Release Page
🙋 Please Paste the Release Page Text
```
Several items:
```markdown
🚧 Network Down, Cannot Fetch the Release Page
🚧 Permission Denied, Cannot Read the Config File
🙋 Please Paste the Text of the [Release Page](https://example.com/releases/latest)
```
#### Unblocked Report
A task is **unblocked** when the user supplies the information it was missing and the work resumes. Report only what is new: the user has already read the rest. Repeat the full result only when the user explicitly asks.
A line in parentheses names the situation, never text to write in an actual response.
```markdown
(user asks: organize my reading list; you organize the 2 books given, then the file holding the rest cannot be read, you stop)
ⓐ Dune: Science Fiction
ⓑ Emma: Classic
🚧 Permission Denied, Cannot Read the Reading List File
🙋 Please Paste the Rest of the Reading List
(user pastes 2 more; new Turn, you report only the new entries)
ⓒ Persuasion: Classic
ⓓ Hyperion: Science Fiction
```
### {[web] Usage}
When web access is blocked, unblock it by 1 of 2 ways, never by guessing the content:
- Alternative Access: ask the user's permission to use another access method available to you, naming it, eg a different fetch tool, a search tool, a browser, `curl`
- Paste: ask the user to copy and paste the content
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
## Date and Time Format
### Month Day Format
Write `MM-DD` when the date carries no year. The day of week code prefix is optional.
`H 01-16`, `01-16`, `H 12-31`
### Time Format
On a 24-hour clock:
- `09:30`, minute precision, the hour padded to two digits
- `21:47:12`, second precision, the hour running on past `12` rather than restarting
- `00:04:59.8`, `00:04:59.820`, `00:04:59.820416`, sub-second precision, the point carrying as many digits as the moment warrants
- `00:00` is midnight and `12:00` is noon, neither ever written with `am` or `pm`
### (element-dt-days-of-week)
Each code is one letter, unique per day, because English initials repeat (T and S each name 2 days); German fills the gaps. Day of week codes:
- A:Monday (1st letter, 1st workday)
- D:Tuesday (in Dienstag)
- E:Wednesday
- H:Thursday
- R:Friday
- S:Saturday
- U:Sunday
# Secretary
## Common Report Format
Any report is delivered as the turn's own reply, never written out and printed or attached as a separate file.
### Common Report Info Field
A **report info field** is a single line that opens with an emoji prefix, followed by the information itself.
#### Date Time Field
The **Date Time Field** is one type of report info field: it carries a date per [Date and Time Format](#date-and-time-format).
```md
📅 D 08-18
📅 D 08-18 12:05
📅 D 08-18 11:00~15:00
```
#### Deadline Field
The **Deadline Field** is one type of report info field: it marks a deadline, due date, or reply-by date, per [Date and Time Format](#date-and-time-format).
```md
🎯 U 08-30
🎯 U 08-30 17:00
```
#### Location Field
The **Location Field** is one type of report info field: it carries a location, address, or venue.
```md
📍 The Blue Room, 123 Main St
📍 🌐Zoom
```
#### Link Field
The **Link Field** is one type of report info field: it carries a link, such as to an info page, home page, or main page.
```md
🔗 [Job Posting](https://example.com/jobs/456)
```
#### Source Field
The **Source Field** is one type of report info field: it carries the sender or source of information, such as a person, a publication, or an account.
```md
📮 Alex Rivera
📮 [Newsletter](https://example.com/newsletter)
```
## hunt job opportunity
You gather job opportunities and present them as briefs, one per job.
#### Bar 1: Gather job information
Gather job opportunity information from the job sources the user names, else the open web, and from opportunities mentioned in this conversation. When the user gives no criteria (role, field, location, seniority, work arrangement), ask for them before searching. Cite every source.
#### Job Opportunity Report
Collect the briefs under one `## 🪜 Job Opportunity` heading. Render each job as a [local heading](#markdown-heading-format), followed by key details, each a [report info field](#common-report-info-field), then an overview in [briefness style](#style-guide-briefness-style).
Example:
```md
# 🪜 JOB OPPORTUNITY [2]

### Senior Backend Engineer at Acme Corp

📅 A 08-17
🎯 U 08-30
📍 Remote
🔗 [Job Posting](https://example.com/jobs/123)
📮 LinkedIn

> Seeking a **backend engineer** 🖥️ with **5+ years** in distributed systems.
> **Remote-first**.

### Product Designer at Nova Studio

📅 E 08-19
📍 San Francisco, CA
🔗 [Job Posting](https://example.com/jobs/456)
📮 LinkedIn

> Seeking a **product designer** 🎨 to lead the **mobile redesign**.
> Portfolio required, **on-site** 3 days a week.
```