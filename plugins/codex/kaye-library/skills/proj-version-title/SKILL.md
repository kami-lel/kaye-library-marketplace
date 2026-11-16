---
name: proj-version-title
description: 'Writes a version release title from new vs. old version: bump word, release type, version.'
when_to_use: 'Naming a version release: "title this release", "what do I call 1.0.0", Prototype, Pre-Alpha, Alpha, Beta, Release Candidate, or Stable label, major/minor/patch bump word. Not for choosing the version number itself'
metadata:
  version: 1.4.1
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
A version title names a version release: `<Bump> <Release Type> <version>`. It depends on the [bump word](#semantic-version-bump), which drops out when the new version has no bump.
##### release type
Check the new version against these rows in order; the first match wins:
| Version | Release Type |
|---|---|
| contains `-alpha` | Alpha Release |
| contains `-beta` | Beta Release |
| contains `-rc` | Release Candidate |
| `0.9.z` | Pre-Alpha Release |
| `0.5.z`~`0.9.z`, only when Vertical Slice is enabled | Vertical Slice Release |
| `0.y.z` | Prototype Release |
| `x.y.z` | Stable Release |
Write no bump word on alpha, beta, or release candidate titles: the tag already states the stage.
##### examples
| New | Old | Title |
|---|---|---|
| `0.3.2` | `0.3.1` | `Patch Prototype Release 0.3.2` |
| `0.9.3` | `0.9.2` | `Patch Pre-Alpha Release 0.9.3` |
| `1.0.0-beta.2` | `0.9.0` | `Beta Release 1.0.0-beta.2` |
| `1.0.0` | `0.9.0` | `Major Stable Release 1.0.0` |
| `1.1.0` | `1.0.0` | `Minor Stable Release 1.1.0` |
| `1.1.1` | `1.1.1` | `Stable Release 1.1.1` |