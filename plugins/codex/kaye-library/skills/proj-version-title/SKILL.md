---
name: proj-version-title
description: 'Writes a version release title from new vs. old version: `BUMP TYPE VERSION`.'
when_to_use: 'Naming a version release: "title this release", "what do I call 1.0.0", Prototype, Pre-Alpha, Alpha, Beta, or Release Candidate label, major/minor/patch bump word. Not for choosing the version number itself'
metadata:
  version: 1.6.2
---

# Projects
## Project Semantic Version
- **core:** `major.minor.patch` / `x.y.z`
- pre-release: append `-` plus dot-separated identifiers, e.g. `x.y.z-alpha`, `x.y.z-alpha.2`. identifiers must use `[0-9a-z-]` only; no uppercase, no empty identifiers.
- build: append `+` plus dot-separated identifiers, e.g. `x.y.z+build.1`, `x.y.z-alpha+build.1`; identifiers must use `[0-9A-Za-z-]` only
### semantic version bump
A **semantic version bump** is the part of the version core (major, minor, patch) the new version raised over the old one. Compare the two cores:
| Bump | When |
|---|---|
| Major | `x` is higher |
| Minor | `y` is higher, `x` equal |
| Patch | `z` is higher, `x` and `y` equal |
Where none holds (equal, lower, or either side not `x.y.z`), the version has no bump.
### Semantic Version Title
Write the title of a version release as `BUMP TYPE VERSION`:
1. Find BUMP: compare the new version with the old one, per [semantic version bump](#semantic-version-bump).
2. Find TYPE: look up the new version in the table below.
Drop BUMP when the new version has no bump. TYPE is never dropped.
##### release type
Check the new version against the rows from top to bottom. Stop at the first match.
| Version | Type |
|---|---|
| contains `-alpha` | Alpha Release |
| contains `-beta` | Beta Release |
| contains `-rc` | Release Candidate |
| `0.9.z` | Pre-Alpha Release |
| `0.5.z`~`0.8.z`, only when Vertical Slice is enabled | Vertical Slice |
| `0.y.z` | Prototype |
| `x.y.z` | Release |
##### examples
| New | Old | Title |
|---|---|---|
| `0.3.2` | `0.3.1` | `Patch Prototype 0.3.2` |
| `0.9.3` | `0.9.2` | `Patch Pre-Alpha Release 0.9.3` |
| `1.0.0-beta.2` | `0.9.0` | `Major Beta Release 1.0.0-beta.2` |
| `1.0.0-rc` | `1.0.0-beta.2` | `Release Candidate 1.0.0-rc` |
| `1.1.0` | `1.0.0` | `Minor Release 1.1.0` |