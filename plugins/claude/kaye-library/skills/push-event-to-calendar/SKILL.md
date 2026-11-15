---
name: push-event-to-calendar
description: Adds an event to the user's outside calendar app or service, from a single supplied event or from an event list already organized in the conversation.
when_to_use: Trigger on "add this to my calendar," "put these events on my calendar," "schedule this," or once an event list has been assembled in conversation and needs to land on the calendar. Trigger even w/o explicit ask whenever a firm, dated event surfaces in conversation that the user would plausibly want on the calendar. Not for pulling or checking existing calendar events
metadata:
  version: 1.3.2a0
---

# Secretary
## calendar management
Default sub-calendars, to adapt: replace or extend them with the user's own sub-calendars when given:
- Business (work matters at the user's own workplace: in-team information, vendor and client dealings, invoicing and billing, contracts and partnerships, and project and deal coordination)
- Career (job search and professional advancement: applications, recruiter outreach, interviews, offers, and job market activity)
- Education (academic life: coursework, instruction, evaluation, and the institutional matters that surround them)
- Entertainment (leisure and recreation consumed or attended for enjoyment, not tied to a specific relationship; example: a concert, a movie screening, a board game night)
- Faith (religious and fellowship life: worship, spiritual growth, and the practices that carry them)
- Optional (events the user may attend or skip without consequence, not yet firmly committed; example: a coffee invite with no RSVP given, a neighbor's open house)
- Private (personal life with a real individual, not a bot or organization: relationships, one-on-one contact, and the exchanges shared with them)
- Public (fallback sub-calendar for an event that matches no more specific sub-calendar; example: a city's fireworks show, a library's public lecture)
----
Aggressively replace the full form with its shorthand:
- asgn:assign,assignment
- hw:homework
- mtg:meeting
### Push Event to Calendar
Movement 1~2, in strict order: each fully finished, with nothing skipped or reordered, before the next begins.
- Movement 1: Build event table per [Event Table](#event-table). Present it to the user & hold: push no event before the user confirms; the user may pick a subset by id per [Alphabetical Sequence Numbering in Chat](#alphabetical-sequence-numbering-in-chat)
- Movement 2: Confirm w/ user, then push: call the Create or Update tool per event
Optional, below the table: a bullet per event needing extra detail.
##### Event Table
The table holds each event's state, never what to change on it.
Example:
```md
| id | Event | 📅 | 📍 | Calendar | Remark |
| --- | --- | --- | --- | --- | --- |
| ⓐ | Jazz Night at the Blue Room | R 08-28 20:00 | The Blue Room, 123 Main St | Entertainment | Live jazz w/ house quartet & guest vocalist |
| ⓑ | Thesis Workshop | R 08-28 14:00~16:00 | 🌐Zoom | Education | Moved from Thu to Fri |

- ⓐ Repeats weekly on Thu, starts 08-28, ends 10-30 · [Event Page](https://example.com/jazz-night)
- ⓑ 🌐 [Zoom Meeting](https://zoom.us/j/1234567890)
```
#### {[Claude:GoogleCalendar:EventEdit] Usage}
Movement 2: Call `GoogleCalendar:create_event` per new event: carry date, time, location & brief description from source.
Event exists already, detail only changed: call `GoogleCalendar:update_event` instead
#### {[Claude:iOS:Calendar:EventEdit] Usage}
Movement 2: Call `event_create_v1` per new event: carry date, time, location & brief description from source.