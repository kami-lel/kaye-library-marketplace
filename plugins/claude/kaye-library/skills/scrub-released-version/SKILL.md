---
name: scrub-released-version
description: 'Scrubs up after a version release: reports the release, then, each on approval, pushes `main` and its `v` tag, prunes merged branches, fast-forwards `dev` to `main`, and bumps `dev` to the next patch alpha.'
when_to_use: 'Reach for this once a release is merged into `main` and tagged: "push the release," "clean up after the release," "sync dev with main," "open the next alpha on dev." Not for cutting the release itself (use the release-version skill) or pruning branches alone (use the prune-merged-branches skill).'
metadata:
  version: 1.5.1
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
## Scrub After Version Release
Once the release is merged into `main` and tagged, scrub what it left behind: publish `main` and the tag, prune merged branches, bring `dev` level with `main`, and open the next version on `dev`. Each step waits for the user's approval, since a push publishes and a pruned branch cannot be recovered by name.
Learn the release first:
- version: settled in the conversation, else the `v` tag on `main`'s tip, read with `git describe --tags --exact-match main`
- title: that version's [Semantic Version Title](#semantic-version-title), eg `Minor Release 1.1.0`
#### Movement 1: Report and Ask Approval
Reply as below, asking 4 approvals: push `main` and the tag, prune merged branches, naming each branch to prune (the candidates of [Prune Merged Branches](#prune-merged-branches)), fast-forward `dev` to `main`, local and remote, and bump `dev` to the next alpha, naming that version.
The next alpha raises the released patch by 1 and appends `-alpha`, eg `1.2.5` opens `1.2.6-alpha`, so `dev` never claims a released version.
<post-release-output-example>
🚩🐙 Minor Release 1.1.0
✍️ ⓑ push `main` and `v1.1.0` to origin?
✍️ ⓒ prune merged branches `add-search-filter`, `fix-login-redirect`?
✍️ ⓓ fast-forward `dev` to `main`, local and origin?
✍️ ⓔ bump `dev` to `1.1.1-alpha`, local and origin?
ⓐ all of above
</post-release-output-example>
#### Movement 2: Push, Prune, and Sync Dev
Run only the approved actions, in order; ⓐ approves all four:
- ⓑ `git push origin main vVERSION`
- ⓒ invoke `prune-merged-branches`
- ⓓ fast-forward `dev` to `main`, local and origin; if it cannot fast-forward, report in one line and stop
- ⓔ only after ⓓ succeeds (else skip, saying why): on `dev`, set the next alpha in every version metadata file, commit per [Commit Sense](#commit-sense), then `git push origin dev`
Reply once, after all are done:
<post-push-prune-output-example>
🚩🐙 pushed `main` and `v1.1.0` to origin
🚩🐙 pruned `add-search-filter`, `fix-login-redirect`
🚩🐙 fast-forwarded `dev` to `main`, local and origin
🚩🐙 bumped `dev` to `1.1.1-alpha`, local and origin
</post-push-prune-output-example>
### {[Claude:Skill] Usage}
Invoke `prune-merged-branches` and `commit-sense` skills via `Skill` tool.