---
name: proj-version
description: 'Defines the semantic versioning scheme: how MAJOR, MINOR, and PATCH numbers are chosen and written.'
when_to_use: 'Any version-number decision: "what version is next", "bump the version", semver, pre-release tags, or a breaking-change release.'
metadata:
  version: 1.6.2
user-invocable: false
---

## Project Semantic Version
- **core:** `major.minor.patch` / `x.y.z`
- pre-release: append `-` plus dot-separated identifiers, e.g. `x.y.z-alpha`, `x.y.z-alpha.2`. identifiers must use `[0-9a-z-]` only; no uppercase, no empty identifiers.
- build: append `+` plus dot-separated identifiers, e.g. `x.y.z+build.1`, `x.y.z-alpha+build.1`; identifiers must use `[0-9A-Za-z-]` only