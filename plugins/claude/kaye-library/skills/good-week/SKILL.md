---
name: good-week
description: Runs the user's weekly look ahead, events and job opportunities alike, closing with a single report.
when_to_use: Trigger on "good week," a weekly or start-of-week check-in request, or an ask for what is coming up this week.
metadata:
  version: 1.3.2a0
---

## Good Week
You run the user's weekly look ahead: scan the event radar across the coming week, hunt job opportunities with sources cited, and report what survives the filter. You follow [scan event radar](#scan-event-radar) and [hunt job opportunity](#hunt-job-opportunity), as written.
This run works the radar and the job hunt: [Good Morning](#good-morning) owns the inbox.
#### Procedure
Bar 1~3, in strict order: each fully finished, with nothing skipped or reordered, before the next begins.
- Bar 1: Gather events. Run Bar 1: Gather event of week of [scan event radar](#scan-event-radar)
- Bar 2: Hunt job opportunities. Run Bar 1: Gather job information of [hunt job opportunity](#hunt-job-opportunity), searching the job sources the user names, else the open web, and citing every source
- Bar 3: Report. Run Bar 2 of [scan event radar](#scan-event-radar) to format the gathered events and the Job Opportunity Report of [hunt job opportunity](#hunt-job-opportunity) to format the gathered opportunities, then emit the report per [Good Week Reporting](#good-week-reporting)
----
The weekly view carries the whole week entire, an event or job opportunity a daily run already surfaced included.
#### Good Week Reporting
One Markdown document: the event briefs entire, ordered by date, soonest first, job opportunities following, each with its sources cited.
Example, abridged: only the heading structure is shown; `...` replaces each entry's key details and overview.
```md
# 🗓️ Good Week Report

# 📡 EVENT RADAR [4]

### Rooftop Mixer This Saturday

...

----

# 🪜 JOB OPPORTUNITY [1]

### Backend Engineer at Acme Corp

...
```
### {[Claude:Skill] Usage}
Invoke `scan-event-radar-weekly`, then `hunt-job-opportunity`, via `Skill` tool.