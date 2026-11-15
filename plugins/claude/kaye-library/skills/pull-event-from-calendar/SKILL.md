---
name: pull-event-from-calendar
description: Retrieves existing events from the user's outside calendar app or service into the conversation, so the conversation can work against the user's actual schedule.
when_to_use: Trigger on "what's on my calendar," "check my schedule," "am I free," or any task needing the user's real calendar state. Trigger even w/o explicit ask whenever a request turns on a date, time, or conflict the conversation cannot answer without the user's actual calendar. Not for adding or scheduling new events
metadata:
  version: 1.4.0
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
### Pull Event from Calendar
#### {[Claude:GoogleCalendar:EventInfo] Usage}
Call `GoogleCalendar:search_events` per request scope: date range, keyword, or both.
Single known event needing full detail: call `GoogleCalendar:get_event` instead
#### {[Claude:iOS:Calendar:EventInfo] Usage}
Call `event_search_v0` per request scope: date range, keyword, or both.