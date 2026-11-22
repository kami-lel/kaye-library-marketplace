---
name: maintain-changelog
description: Use this skill when the user wants to add, fix, or reorganize entries in an existing CHANGELOG — logging new features, bug fixes, or breaking changes without overwriting existing content. Trigger even for casual requests like "update the changelog" or "log what changed."
when_to_use: Trigger on "update the changelog", "log what changed", "add a changelog entry", or "fix a changelog entry".
metadata:
  version: 1.5.1
---

## Style Guide Briefness Style
- write in **newspaper headlinese**, prioritize brevity over grammar
- use present for current, infinitive for planned
- omit articles (a, an, the) and helper verbs, use strong nouns, verbs
- compress with punctuation: colon, dash, comma, otherwise minimize, no terminal periods
- use numerals (use 2, not two), symbols, common abbreviations when unambiguous
- prefer active voice
- keep sentences short, direct, drop filler
Aggressively replace the full form with its shorthand:
- vs.:against
- &:and
- ~:and the others (eg a, b, ~)
- ~~:and the others (eg a, b, ~~; use when ~ is ambiguous)
- ⇐:because,caused by,result of
- ←:become/change/transform from
- →:become/change/transform into
- b/t:between
- cf.:confer,compare
- ↓:decrease,decrement
- 〃:ditto,repetitive as above/before
- e.g.:example
- iff:if and only if
- re:in the matter of,concerning,regarding
- ↑:increase,increment
- misc.:miscellaneous
- n/a:not applicable
- №:number
- \:of
- /:or
- ~:range (eg 1~5, a~f, ii~iv)
- 〃:same as cell above
- i.e.:that is,in other words
- ⇒:therefore,causing,resulting
- ※:which see,reference to
- w/:with
- w/i:within
- w/o:without
## Style Guide Good Writing
- Correct spelling, grammar, punctuation, sentence structure, and verb tense errors.
- Preserve the original meaning, voice, tone, style, word order, and vocabulary as much as possible unless the user requests heavier rewriting.
- Make only the minimum changes needed to improve correctness, readability, and clarity.
- Ensure the revised text is clear, polite, and free of language errors.
- Use American English by default, but if the original text clearly uses another spelling convention, preserve that convention.
- Expand uncommon abbreviations only when doing so improves clarity.
- Do not add new information, remove intended information, or change the substantive meaning of the text.
- Avoid generic filler when details are unavailable
- Avoid dense prose, generic filler, and unnecessary complexity
# Projects
## Project Semantic Version
- **core:** `major.minor.patch` / `x.y.z`
- pre-release: append `-` plus dot-separated identifiers, e.g. `x.y.z-alpha`, `x.y.z-alpha.2`. identifiers must use `[0-9a-z-]` only; no uppercase, no empty identifiers.
- build: append `+` plus dot-separated identifiers, e.g. `x.y.z+build.1`, `x.y.z-alpha+build.1`; identifiers must use `[0-9A-Za-z-]` only
### Semantic Version Extended
##### common pre-releases
- pre-releases types: `alpha`, `beta`, `rc`
- first pre-release: use unnumbered form, e.g. `1.0.0-alpha`.
- next pre-releases: start at `.2`, e.g. `1.0.0-alpha.2`, `1.0.0-alpha.3`, **do not use:** `1.0.0-alpha.1`
- pre-release patch: e.g. `1.0.0-alpha.2.1`
##### common build metadata
- `1.0.0+Win`, `1.0.0+mac`, `1.0.0+linux`: builds for different OS
- `0.5.0+2026-01-01-1234`, `1.0.0-alpha.2+2026-01-01`: date / date-time builds
##### development stage examples
- toy/prototypes: `0.1.z`~`0.4.z`
- Vertical Slice (VS): `0.5.z`~`0.8.z`
- pre-alpha: `0.9.z`
- alpha: `1.0.0-alpha`, `1.0.0-alpha.2`, ~~
- beta: `1.0.0-beta`, `1.0.0-beta.2`, ~~
- Release Candidate (RC): `1.0.0-rc`, `1.0.0-rc.2`
- first Stable Release: `1.0.0`
## Repository CHANGELOG Writer
these guidelines define what a good `CHANGELOG.md` (or CHANGELOG-style file) is
#### Guiding Principles
Changelogs are *for humans*, not machines.
- write entries a reader can act on, per [Style Guide Good Writing](#style-guide-good-writing)
- hold each entry to one terse line, per [Style Guide Briefness Style](#style-guide-briefness-style)
- format headings, lists, and callouts per [Style Guide Markdown Format](#style-guide-markdown-format)
Structure:
- group the same types of changes together
- keep every version and section linkable, with a links block at the foot of the file holding all of them
- keep an `[Unreleased]` section carrying all six subsections, even when empty
- omit empty subsections from released versions
Versions:
- carry every version, latest first, numbered per [Project Semantic Version](#project-semantic-version)
- show the release date beside each version
#### Types of Changes
- `Added`: new features
- `Changed`: changes in existing functionality
- `Deprecated`: soon-to-be removed features
- `Removed`: now removed features
- `Fixed`: any bug fixes
- `Security`: in case of vulnerabilities
#### CHANGELOG Example
```md
# Example Repository CHANGELOG

## [Unreleased]
### Added
### Changed
### Deprecated
### Removed
### Fixed
### Security

[unreleased]: https://github.com/example-user/example-project/compare/v2.0.0...dev

## [2.0.0] - 2024-01-15

### Removed

- Node 14 runtime support

> [!WARNING]
> Drops support for Node 14; upgrade before updating
[2.0.0]: https://github.com/example-user/example-project/compare/v1.5.7...v2.0.0

## [1.5.7] - 2023-12-04

### Fixed
- Profile picture not rendering correctly on Safari

[1.5.7]: https://github.com/example-user/example-project/compare/v1.5.6...v1.5.7

## [1.5.6] - 2023-11-02

### Added

- OAuth2 support for Google and GitHub providers

> [!CAUTION]
> Profile pictures fail to render on Safari; fixed in [1.5.7]

[1.5.6]: https://github.com/example-user/example-project/releases/tag/v1.5.6
```
## Maintain CHANGELOG
1. take what to log from the conversation and recent repository changes
2. file each entry under the right subsection of `[Unreleased]`, the default target for new work
3. combine with existing entries rather than duplicating; leave their wording as it stands
4. keep the links block current so every version stays referenced
5. edit in place
6. update the CHANGELOG in place, then return a brief summary of the changes, per [Repository CHANGELOG Writer](#repository-changelog-writer), [Style Guide Markdown Format](#style-guide-markdown-format), and [Style Guide Good Writing](#style-guide-good-writing)