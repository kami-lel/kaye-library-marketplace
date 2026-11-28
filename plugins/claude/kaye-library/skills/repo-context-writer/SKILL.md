---
name: repo-context-writer
description: '`CONTEXT.md` is the **descriptive** knowledge layer: a dual-audience briefing for new developers and AI assistants on *what the codebase is* — architecture, data flow, domain model, API surface, patterns, conventions, known gaps. It goes deeper than the setup-focused `README.md` and is the foundational map other files build on; `CONTEXT.local.md` holds personal, gitignored context. This skill writes and maintains both.'
when_to_use: 'Use to create, update, or review `CONTEXT.md` or `CONTEXT.local.md`, or to capture durable codebase knowledge for AI across sessions. Triggers: "write a CONTEXT.md," "document the architecture for AI," "briefing doc for the repo." Difference from its sibling: `CONTEXT.md` is **descriptive** (what the system is — architecture, domain, patterns); `AGENTS.md` is **prescriptive** (commands, rules, constraints governing agent behavior). Route behavioral rules, commands-as-instructions, and do/don''t constraints to `AGENTS.md`, not here.'
metadata:
  version: 1.6.2
paths:
- '**/{CONTEXT,Context,context}{,.local}{,.md}'
---

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
A scoped `CONTEXT.md` or a local `CONTEXT.local.md` follows the same format, standard, and style, per [Project Context Engineering](#project-context-engineering).
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