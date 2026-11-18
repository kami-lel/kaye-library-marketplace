---
name: element-dt-time-format
description: Formats a time of day on a 24-hour clock, precision from minute down to sub-second
when_to_use: 'Any output time of day: schedules, meetings, alarms, timestamps, log entries, span endpoints, any hour stated as 3pm or noon. Not the date beside it'
metadata:
  version: 1.5.0
---

### Time Format
On a 24-hour clock:
- `09:30`, minute precision, the hour padded to two digits
- `21:47:12`, second precision, the hour running on past `12` rather than restarting
- `00:04:59.8`, `00:04:59.820`, `00:04:59.820416`, sub-second precision, the point carrying as many digits as the moment warrants
- `00:00` is midnight and `12:00` is noon, neither ever written with `am` or `pm`