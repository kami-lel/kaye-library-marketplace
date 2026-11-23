---
name: condense-agents-and-context
description: 'Shrinks an existing AGENTS and CONTEXT pair: reads both whole, drops finished plans, dead workflows, superseded detail, anything the code already answers, tightens the rest, adds nothing'
when_to_use: 'Fires when the pair has outgrown its content: an `AGENTS.md` too long to keep in context, a "Planned" or "In Progress" or "Migration" section describing finished work, a directory tree the source now contradicts, one rule stated in both files. Also "AGENTS.md is 600 lines", "cut CLAUDE.md down", "why is CONTEXT.md so long". Apply unasked before a release or handoff. Not when new work needs recording'
metadata:
  version: 1.6.0
---

## agents writer
Apply these rules to `AGENTS.md`, formatting it per [Style Guide Markdown Format](#style-guide-markdown-format).
Suggested Sections go under clear `##` headings: use what fits, omit rather than pad, and add any section carrying a project-specific behavioral rule. Keep content to rules and constraints an agent acts on. Each writer below lists its own.
The root `AGENTS.md` links every file under `docs/`, per [Reference Link Format](#reference-link-format), each phrased to send an agent there when its topic arises.
#### AGENTS Title & Preface
```markdown
# Example Project AGENTS

Prescriptive rules for agents working in this project.

- Belongs Here: rules an agent must follow, ie commands, conventions, constraints, who decides; only what an agent cannot infer from the code
- Size: stay lean for the context window; when the file grows, move detail to `docs/` or cut it
- Upkeep: update in the same change that moves a command, convention, or constraint
- Structure: follow the existing sections; keep every rule true for every contributor
- Belongs in `CONTEXT.md`: descriptive knowledge of the system, ie architecture, domain model, patterns, known gaps
- Belongs in `docs/`: system documentation for users and agents alike; link it from here, never grow this file to hold it
- Local Layer: put machine-specific or personal rules in `AGENTS.local.md`; create it if missing, never commit it
```
Replace `Example Project` with the real project name. Copy the preface exactly, word for word.
The personal layer's title line, marked as local:
```markdown
# Example Project local AGENTS
```
### Repository AGENTS Writer
##### Suggested Sections
Keep content command-oriented; descriptive architecture and domain knowledge belong in `CONTEXT.md`.
- Layout & Naming: where each kind of file goes and how it is named, wherever the repository departs from the standard repository structure or an agent would misplace a file
- Setup Commands: copy-pasteable commands to install, run, and build
- Code Style: conventions this repository actually enforces — typing strictness, quote and semicolon rules, linter and formatter
- Testing Instructions: per the dedicated requirement below
- PR & Commit Instructions: title format, required pre-commit checks, review conventions
- Security Considerations: secrets handling, files and commands never to touch, commands that need confirmation before they run, safety constraints
- Documentation Maintenance: which docs must move when code, commands, or conventions change
- Project Overview & Pointers: one short paragraph, then links to `CONTEXT.md` and the deeper docs. Never duplicate them
Typical additions: release process, migration commands, environment gotchas, do/don't constraints.
In a monorepo, place a nested `AGENTS.md` in each package and state that the file closest to an edited file wins, with chat instructions overriding every file.
##### What to Include
Instruction budget is finite, and a wrong instruction beats no instruction only in the wrong direction. Write for signal:
- document only what an agent cannot infer — skip framework defaults and anything readable from a config file. Pin versions and name non-obvious constraints outright
- favor anti-patterns and counterintuitive rules. "Never use `Y` here, because `Z`" carries signal; "write clean code" carries none
- stay lean and disclose progressively, pointing to nested files, `CONTEXT.md`, or skills rather than crowding the root. Compliance falls sharply past a few dozen rules
- show one real example instead of three paragraphs describing a convention
##### Quality Expectations
- repository-specific, never generic
- behavioral and command-oriented — rules, commands, constraints, not architecture narration
- lean enough to sit in context without crowding out what matters
- explicit about conventions, tooling, and safety constraints
- consistent with existing documentation and repository structure
- free of contributor-facing explanation, which belongs in `README.md`, and descriptive knowledge, which belongs in `CONTEXT.md`
## Repository CONTEXT Writer
You write and maintain `CONTEXT.md` files for software repositories. Apply these rules to `CONTEXT.md` and to a personal `CONTEXT.local.md`, formatting both per [Style Guide Markdown Format](#style-guide-markdown-format).
#### CONTEXT Title & Preface
```markdown
# Example Repository CONTEXT

Descriptive knowledge of this repository for agents and developers.

- Belongs Here: what the system is, ie architecture, domain model, API surface, patterns, known gaps; only what the code cannot show, as it stands, never its history
- Size: stay lean for the context window; when the file grows, move detail to `docs/` or cut it
- Upkeep: update in the same change that moves architecture, patterns, commands, or environment variables
- Structure: follow the existing sections; keep every statement true for every contributor
- Belongs in `AGENTS.md`: prescriptive rules for agents, ie commands, conventions, constraints, do/don't
- Belongs in `docs/`: system documentation for users and agents alike; link it from here, never grow this file to hold it
- Local Layer: put machine-specific or personal context in `CONTEXT.local.md`; create it if missing, never commit it
```
Replace `Example Repository` with the real repository name. Copy the preface exactly, word for word.
The personal layer's title line, marked as local:
```markdown
# Example Repository local CONTEXT
```
#### Suggested Sections
Recommended, not mandatory — use what fits under clear `##` headings, and omit rather than pad. Humans and agents both parse structure faster than prose, so reach for tables, annotated trees, and ASCII diagrams wherever they carry more per token.
- Project Overview: what the app is, who it serves, major tech. A stack table works well
- Repository Layout: annotated tree of landmarks — what each key directory holds and why, not a raw `ls` dump
- Domain Model: entities, primary keys, key fields, foreign-key links. ASCII ERD plus a per-entity table
- API Surface: route prefixes, methods, request and response conventions. Saves reading every route file
- Patterns & Conventions: the highest-value section — where business logic lives, how data access and errors work, which naming to preserve
- Build, Run & Test Commands: exact commands, never descriptions. Lets an assistant verify its own work
- Environment Variables: a table of names, defaults, and descriptions
- Testing Strategy: tools, where tests live, fixture and test-database conventions
- Known Gaps & Constraints: underrated — flag mocked auth, a missing service layer, deliberately pinned-old libraries. Stops a reader building on absent infrastructure
Add any section carrying project-specific knowledge a newcomer or assistant needs — external services, migration flows, key abstractions, historical decisions. A starting point, not a ceiling.
In a monorepo, nest a `CONTEXT.md` per package for its own architecture and domain, the closest file being the most specific. In a large codebase, layer stack-specific patterns and anti-patterns beneath a base `CONTEXT.md`, keeping each file focused before instruction fatigue sets in. Local env quirks, workflow notes, and scratch understanding go in `CONTEXT.local.md`, which augments or overrides the committed shared source of truth without reaching teammates.
#### Living Document Maintenance
A stale briefing is worse than none. Instruct the reader to update the file when entities or services appear, patterns or boundaries shift, build and test workflows change, environment variables are introduced, or conventions are set.
Recommend in-file: update `CONTEXT.md` in the same pull request as the change; have the assistant that just made the change write it, as the final step; and keep the file on the pull-request checklist.
#### Quality Expectations
- repository-specific, never generic
- descriptive — a system map, not a command list
- structured for fast parsing, useful to humans and agents alike
- explicit on patterns, boundaries, and especially known gaps
- current, maintained alongside architecture changes
- complementary to `README.md` and `AGENTS.md`, duplicating neither
## Condense AGENTS and CONTEXT
You work from the **files alone**: no change set, no conversation to draw on, nothing new to add. Every line already there is read once and then kept, shortened, moved, or dropped.
1. read each file whole, judging every section on whether it still earns the space it takes
2. drop what has gone stale: a workflow nobody follows now, a plan already landed or abandoned, a migration finished, an implementation detail the code has since moved past
3. drop what the code already answers on its own — restated file trees, signatures, config values, anything a reader would check in the source before believing the document
4. merge what repeats within a file, and move anything sitting on the wrong side of the pair to its counterpart rather than restating it
5. shorten what survives: same meaning, fewer words, AGENTS directive and imperative, CONTEXT descriptive and explanatory
6. hold AGENTS lean enough to stay in context: the commands an agent must run and the rules it must obey, nothing more
7. hold CONTEXT to what explains the system as it stands, never to how it came to stand that way
8. add nothing the files did not already carry; name a gap you find in your summary rather than filling it
9. update the files in place, then return a brief summary of the changes, per [Repository AGENTS Writer](#repository-agents-writer), [Repository CONTEXT Writer](#repository-context-writer), [Style Guide Markdown Format](#style-guide-markdown-format), and [Style Guide Good Writing](#style-guide-good-writing)