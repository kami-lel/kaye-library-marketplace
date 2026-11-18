---
name: coder-comment-banner-in-code-comment
description: writes comment banners inside source code — ranked heading-plus-ruler separators marking file titles, top-level sections, and nested subsections behind each language's comment leader
when_to_use: 'Any long source file needing structural markers: section dividers, boxed file-title blocks, or banner comments. Trigger on "CB0"–"CB5", "banner", "section header comment", "ruler", and whenever authored code runs long enough that navigation suffers — even without an explicit ask. Not for terminal or logging output.'
metadata:
  version: 1.5.0
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
### CB in Code Comment
Use CB to mark sections of long source files.
**Comment leader** — the ruler follows the language's comment leader (`//`, `#`, ...), so the banner sits inside a normal comment line or block.
**Default** — `L` is the default in **comments**; a bare token reads as its `L` variant (`CB1` ≡ `CB1L`). `CB0`'s inner title line defaults to `L` as well.
**Comment example**:
```cpp
    /*
    ################################################################################
    # stats_demo.cpp
    #
    # produce statistics
    ################################################################################
    */
// constants  ##################################################################
const int kValues[] = {10, 20, 30};

// auxiliaries  ################################################################
// number helpers  =============================================================
double compute_average(const int* v, int n) {
    // accumulate  *************************************************************
    ~~
}

// Entry Point  ################################################################
int main() { ... }
```
```python
    # Public API  ##################################################################
    def to_int(s):
        # quick parse  -------------------------------------------------------------
        ~~
```
`CB0` boxes the file title, `CB1` marks top-level sections, `CB2`/`CB3` nest below. The `# quick parse  ----` line is a **CB5** used off-hierarchy: a small local label, not a structural boundary.