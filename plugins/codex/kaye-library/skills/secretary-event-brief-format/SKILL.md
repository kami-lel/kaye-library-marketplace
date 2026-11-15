---
name: secretary-event-brief-format
description: 'Formats a set of events into `## 📡 Event Radar` briefs: an Event Heading, emoji-prefixed Key Details, and a briefness-style Event Overview per event.'
when_to_use: Trigger whenever a set of events needs presenting as formatted briefs. Not for gathering or filtering events themselves.
metadata:
  version: 1.4.0
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
#### Ticket Field
The **Ticket Field** is one type of report info field: it carries a price, or marks the event as free or RSVP-only.
```md
🎟️ $10
🎟️ $10 [Buy](https://example.com/events/456/tickets)
🎟️ 🆓Free [📩RSVP](https://example.com/events/456/rsvp)
```
### event brief format
Collect the briefs under one `## 📡 Event Radar` heading. Render each event as **Event Heading** + **Key Details** + **Event Overview**:
- **Event Heading**: circled letter per [Alphabetical Sequence Numbering](#alphabetical-sequence-numbering), then the event's name exactly as given, rendered as a [local heading](#markdown-heading-format)
- **Key Details**: one report info field per fact, in this order, each optional, appearing only if the event has that info
  1. date/time, per [Date Time Field](#date-time-field)
  2. location, per [Location Field](#location-field)
  3. ticket/admission info, per [Ticket Field](#ticket-field)
  4. link, per [Link Field](#link-field)
- **Event Overview**: a concise overview per [briefness style](#style-guide-briefness-style)
  - use multiple lines; prefer short line width for each line
  - do not repeat information already covered by Key Details
  - use **bold** for key words
  - add expressive emojis within the text where relevant
##### example
Each report info field follows [Common Report Info Field](#common-report-info-field).
```md
# 📡 EVENT RADAR [2]

### ⓐ Jazz Night at the Blue Room

📅 R 08-28 20:00
📍 The Blue Room, 123 Main St
🎟️ $15 [Buy](https://example.com/tickets)
🔗 [Event Page](https://example.com/jazz-night)

> A **relaxed** evening of live jazz 🎷,
> with the house quartet plus a guest vocalist 🎤.
> Doors open 30 minutes early; seating is first-come.

### ⓑ Saturday Farmers Market

📅 S 08-29 09:00~13:00
📍 Civic Plaza
🎟️ 🆓Free [📩RSVP](https://example.com/farmers-market/rsvp)

> Weekly **outdoor market** 🌻 with local produce,
> baked goods & live music.
> Dog-friendly 🐶, rain or shine.
```