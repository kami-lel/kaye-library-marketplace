---
name: element-dt-watch-day
description: Defines the Watch Day, a day kept on a 30-hour clock that runs past midnight rather than ending at it
when_to_use: Any WD or SWD, any moment falling in the small hours, and any reckoning of which day a late-night task, log entry, or event belongs to
metadata:
  version: 1.3.2a0
---

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