---
name: element-dt-year-month-day-format
description: Formats a date carrying a year, day of week prefix optional
when_to_use: 'Any output date whose year is known or matters: deadlines, timestamps, log entries, filenames, historical dates, spans crossing a year boundary'
metadata:
  version: 1.5.0
---

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