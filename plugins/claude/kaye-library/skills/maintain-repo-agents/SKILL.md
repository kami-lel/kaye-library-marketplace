---
name: maintain-repo-agents
description: Updates an existing repository `AGENTS.md` against what changed, editing in place
when_to_use: 'Triggers: "update AGENTS.md", "CLAUDE.md still says the old path", changed build/test command or convention'
metadata:
  version: 1.4.1
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
### Maintain Repository AGENTS
You work from a **change set**: what the conversation and the repository have altered since the file was last written. A section the change set never reaches is left exactly as it reads.
1. edit in place: fold moved commands, conventions, and constraints into the sections already there, correct what the change set falsified, delete only what it retired
2. leave sound wording, structure, and length alone; descriptive knowledge belongs in `CONTEXT.md`
3. verify facts against the codebase; keep the root file primary and nested files scoped to their package
4. create a missing file only where the change set requires it
5. follow [Repository AGENTS Writer](#repository-agents-writer) and [Style Guide Markdown Format](#style-guide-markdown-format), then return a brief summary of the changes