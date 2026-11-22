---
name: recap-yesterday
description: 'Recaps what user finished yesterday as one warm, encouraging Recap Line: events attended, mail answered, tasks closed, gathered from record & reported to cheer the user toward doing more.'
when_to_use: Trigger on "what did I do yesterday," a recap, review, or standup-note request covering the day before, or any ask for yesterday's finished work. Not for planning ahead, nor today's progress.
metadata:
  version: 1.5.1
---

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
### Time Format
On a 24-hour clock:
- `09:30`, minute precision, the hour padded to two digits
- `21:47:12`, second precision, the hour running on past `12` rather than restarting
- `00:04:59.8`, `00:04:59.820`, `00:04:59.820416`, sub-second precision, the point carrying as many digits as the moment warrants
- `00:00` is midnight and `12:00` is noon, neither ever written with `am` or `pm`
### Watch Day
- SWD:strict watch day (a 24-hour span, running 06:00 to 06:00 the next natural day; consecutive strict Watch Days tile without gap or overlap, so every instant belongs to exactly one)
- WD:watch day (a 30-hour span, running 00:00 to 06:00 the next natural day; consecutive Watch Days overlap across 00:00~06:00, so a task logged at 03:00 belongs to both this Watch Day and the one before it)
A Watch Day carries the small hours of the following morning rather than ending at midnight. Those hours keep the earlier date and count on from 24, up to the Cutoff at 06:00, where the new date takes over and the time is written normally again.
Natural time on the left, the same instant written as a Watch Day on the right:
- 07-02 00:00 = 07-01 24:00, midnight, still counted under 07-01
- 07-02 02:00 = 07-01 26:00, to convert back, subtract 24 from the hour and advance the date
- 07-02 05:59 = 07-01 29:59, the last instant belonging to 07-01
- 07-02 06:00 = 07-02 06:00, past the Cutoff, so it takes the new date, not 07-01 30:00
- 07-02 14:30 = 07-02 14:30, ordinary daytime, left untouched
# Secretary
## daily recap
You report what a [Watch Day](#watch-day) came to, as one warm **Recap Line**: a single encouraging sentence naming what got done, so the day reads back as a win worth building on. A quiet day still gets one encouraging Recap Line, never a blank or a scold.
### {[Claude:GoogleCalendar:EventInfo] Usage}
Call `GoogleCalendar:search_events` scoped to the recapped day's date range. Fold every event returned into the Recap Line; none returned, name no event.
### {[Claude:iOS:Calendar:EventInfo] Usage}
Call `event_search_v0` scoped to the recapped day's date range. Fold every event returned into the Recap Line; none returned, name no event.
### {[Claude:Skill] Usage}
Invoke `pull-task-from-gtd` via `Skill` tool for the recapped day's completed tasks
### {[Hermes:skill_view] Usage}
Load `pull-task-from-gtd` with `skill_view` for the recapped day's completed tasks
### recap yesterday
Task: recap yesterday, per [daily recap](#daily-recap).
##### Reporting
Example:
```md
# 🌙 YESTERDAY RECAP

Yesterday you attended **Thesis Workshop** & closed **3 tasks** on the migration board: a day well spent.
```