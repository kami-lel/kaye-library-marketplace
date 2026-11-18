---
name: ready-release-version
description: 'Cuts a project release: brings `README.md`, `CREDITS.md`, `CHANGELOG.md`, `AGENTS.md`, `CONTEXT.md`, and `docs/` current, moves `[Unreleased]` changelog entries into a dated versioned section, and bumps the version across metadata files like `package.json`, `pyproject.toml`, `Cargo.toml`, or `setup.cfg`.'
when_to_use: Reach for this on release requests — "ship v1.2.3," "cut a release," "tag a version," "bump the version," "prep the release." Not for logging a single in-progress change (use the changelog-maintain skill) or landing a feature branch before merge (use the feature-landing skill).
metadata:
  version: 1.5.0
---

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
## Ready for Version Release
Cut a new release: bring all docs current, finalize the changelog, and bump the project version.
#### Movement 1: Decide Release Version and Date
- require both a version number and a release date; if either is missing, ask the user before proceeding
- the version must match [Project Semantic Version](#project-semantic-version)
#### Movement 2: Maintain the README and CREDITS
Run each in turn, skipping any whose file the repository lacks:
- [Maintain README](#maintain-readme): overview, features, setup, usage, version-dependent details
- [Maintain CREDITS](#maintain-credits): third-party assets added, moved, or removed since the last release
#### Movement 3: Maintain the Docs Directory
Run [Maintain Repository Docs](#maintain-repository-docs): affected files under `docs/`.
#### Movement 4: Condense AGENTS and CONTEXT
Run [Condense AGENTS and CONTEXT](#condense-agents-and-context): changed commands, conventions, constraints, architecture.
While in `CONTEXT.md`, prune as well as update: keep only what describes the released state, and cut superseded plans, stale notes, and history no longer worth a reader's time. The file should end up smaller, not just newer.
#### Movement 5: Condense and Close Out the Changelog
1. run [Condense CHANGELOG](#condense-changelog) to reword `[Unreleased]` entries into changelog style and settle any Admonitions for Breaks and Hazards
2. move every now-condensed `[Unreleased]` entry, admonitions included, into a new versioned section headed with the version and date from Movement 1, keeping only non-empty subsections
3. leave a fresh `[Unreleased]` section above it, carrying every standard subsection heading with no entries beneath
4. update the GitHub comparison links so every version, including the new tag, stays referenced
#### Movement 6: Bump the Repository Version
Set the version to match Movement 1 exactly, in whichever metadata files apply — `setup.cfg`, `pyproject.toml`, `package.json`, `Cargo.toml`, and the like.