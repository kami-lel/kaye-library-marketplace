---
name: good-morning
description: Runs the user's daily morning check in one pass, closing with a single combined report.
when_to_use: Trigger on "good morning," a daily or morning check-in request, or an ask to catch up on daily admin and housekeeping. Not for a single one-off task or an ad-hoc lookup.
metadata:
  version: 1.3.2a0
---

## Good Morning
You run the user's daily morning check in one pass: sweep the unread inbox, recap what yesterday came to, scan the event radar, hunt job opportunities, and deliver a single report. You follow [sweep email inbox](#sweep-email-inbox), [recap yesterday](#recap-yesterday), [scan event radar](#scan-event-radar), and [hunt job opportunity](#hunt-job-opportunity) as written, including every Judgment Note and Safety Constraint each carries.
Mail is itself an event and job source. Some messages carry an invitation, a talk announcement, an opening, or a dated deadline; Bar 8 takes events out of the mail, Bar 9 takes job openings out of the mail, and Bar 10 presents both alongside the radar's and hunt's own.
#### Procedure
Bar 1~10, in strict order: each fully finished, with nothing skipped or reordered, before the next begins.
- Bar 1~6: Sweep. Run Bar 1~6 of [sweep email inbox](#sweep-email-inbox), with one change at Bar 6: raise no separate report, and hold the swept, categorized, flagged result for Bar 10
- Bar 7: Recap yesterday. Run [recap yesterday](#recap-yesterday) whole, and hold its lines for Bar 10
- Bar 8: Gather events. Run Bar 1: Gather event for today of [scan event radar](#scan-event-radar) over the radar's event sources, then add every event carried by mail read in Bar 2. Keep each mail-borne event tied to its message, so Bar 10 can attribute and link it
- Bar 9: Hunt job opportunities. Run Bar 1: Gather job information of [hunt job opportunity](#hunt-job-opportunity) over everything gathered in Bar 1~8, mail included. Keep each mail-borne opportunity tied to its message, so Bar 10 can attribute and link it
- Bar 10: Report. Run Bar 2 of [scan event radar](#scan-event-radar) to format the gathered events and the Job Opportunity Report of [hunt job opportunity](#hunt-job-opportunity) to format the gathered opportunities, then emit the single report per [Good Morning Reporting](#good-morning-reporting)
----
An event or job opportunity may appear in a message of any category, an Automated newsletter as readily as a Private note. Categorizing a message never excuses it from Bar 8 or Bar 9.
A mail-borne event or job opportunity never replaces its message in the mail half: the message is still reported where its category places it.
#### Good Morning Reporting
One Markdown document: yesterday's recap first, job opportunities second, events third, mail last. A mail-borne event or job opportunity carries `📨` sender and `🪧` message link among its key details; the mail report then follows entire, its headings demoted one level.
Example, abridged: only the heading structure is shown; `...` replaces each entry's key details and overview.
```md
# 🌅 Good Morning Report

# 🌙 YESTERDAY RECAP

...

----

# 🪜 JOB OPPORTUNITY [1]

### Backend Engineer at Acme Corp

...

----

# 📡 EVENT RADAR [2]

### Rooftop Mixer This Saturday

...

----

# 📬 EMAIL INBOX SWEPT [15]

# 🏦 Admin [2\15]

### 💎🚨 Tuition due Friday

...
```