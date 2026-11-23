---
name: coder-comment-banner-in-print-out
description: writes banners into printed program output — ranked heading-plus-ruler dividers separating run titles, execution phases, and nested checks across logs, demos, and test runs
when_to_use: 'any script or program emitting multi-phase terminal output: run headers, stage separators, log-section dividers, demo and test-phase markers. Trigger on "CB0"–"CB5", "banner", "divider", "phase header" alongside print, echo, or logging calls — and whenever generated output spans distinct phases a reader must scan. Not for banners living inside code comments'
metadata:
  version: 1.6.0
---

## Comment Banner
**Comment banners** (CB) expose structure in long output. A banner is a short **heading** plus a **ruler** — one symbol repeated to fill the line to **80 chars**, with two spaces between heading and ruler.
**Levels** — six ranks, highest (`CB0`) to lowest (`CB5`), each fixing one ruler symbol:
| token | ruler | role |
| --- | --- | --- |
| `CB0` | `#` box | file/run Title, boxed between top and bottom rulers; multi-line |
| `CB1` | `#` | top-Level section |
| `CB2` | `=` | sub-Section |
| `CB3` | `*` | sub-Sub-section |
| `CB4` | `+` | finer Group |
| `CB5` | `-` | lowest; also usable freely as a small local Label, off-hierarchy |
**Justification** — suffix `L` / `R` / `C` on any level (`CB1`–`CB5`) sets where the heading sits:
| suffix | layout |
| --- | --- |
| `L` | heading Left, ruler fills right |
| `R` | ruler fills left, heading ends at Col 80 |
| `C` | heading Centered, ruler splits evenly (±1) |
```
CB1L   heading  ##############################…
CB1R   …##############################  heading
CB1C   ###############  heading  ###############
```
**Defaults** — a bare token means the default variant of its medium, which differs between code comments and printed output. `CB0`'s inner title line follows the same rule as the surrounding medium.
**Heading style** — keep it short and name the real block (`parse CLI flags`, not `section 1`). Case by visibility:
- **Title Case** = public / exported interface — `Public API`, `Main Entry Point`, `Properties`, `CLI`, `Public Method`, `Public Attributes`, `Public Fields`
- **lowercase** = internal / implementation detail — `constants`, `auxiliaries`, `private variables`, `private methods`/`attributes`/`fields`
**Use** at genuine boundaries — modules, sections, functions, related groups, output phases — and only when a block is long enough that a separator aids navigation. **Avoid** for line-level or sequential groups inside a function (use plain comments), in ordinary prose, and anywhere frequent enough to become noise.
**Note** — the examples below cluster many banners together to show the full set of levels at once. Real usage is far rarer: reach for CB only to separate genuine functional blocks, modules, or logically distinct sections — never at the density shown there.
### CB in Print Out
Use CB to divide logging / demo / test phases
**Default** — `C` is the default in **printed output**; a bare token reads as its `C` variant. `CB0`'s inner title line follows the same rule.
**Printed output example** — levels nest exactly as in comments:
```
################################################################################
# configkit_demo — load and validate settings
################################################################################
source:  ./config/app.toml
mode:    strict

####################################  load  ####################################
INFO  read 24 keys from app.toml
INFO  merged 3 defaults

##################################  validate  ##################################
====================================  types  ===================================
INFO  port: int OK
INFO  host: str OK
===================================  ranges  ===================================
WARN  port 70000 above max 65535 → clamped
----- warnings -----
WARN  1 value adjusted

###################################  report  ###################################
INFO  config valid, 24 keys ready
```
`CB0` boxes the run title, `CB1C` (`#`) marks each phase (`load`, `validate`, `report`), and `CB2C` (`=`) marks the checks nested under `validate`. The `----- warnings -----` line is again a **CB5**, dropped in freely as a lightweight local marker rather than a ranked phase.