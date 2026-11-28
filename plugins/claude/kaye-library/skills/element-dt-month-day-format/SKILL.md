---
name: element-dt-month-day-format
description: Formats a date carrying no year, day of week prefix optional
when_to_use: 'Any output date stated without a year: anniversaries, birthdays, recurring schedules, near-term plans, entries inside the current year'
metadata:
  version: 1.6.2
---

## Date and Time Format
### Month Day Format
Write `MM-DD` when the date carries no year. The day of week code prefix is optional.
`H 01-16`, `01-16`, `H 12-31`
### (element-dt-days-of-week)
Each code is one letter, unique per day, because English initials repeat (T and S each name 2 days); German fills the gaps. Day of week codes:
- A:Monday (1st letter, 1st workday)
- D:Tuesday (in Dienstag)
- E:Wednesday
- H:Thursday
- R:Friday
- S:Saturday
- U:Sunday