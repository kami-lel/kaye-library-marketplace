---
name: create-project-agents
description: Creates `AGENTS.md` for a generic project that has none
when_to_use: 'Triggers: "write an AGENTS.md for this project", "add agent instructions", "set up agent rules"'
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
### Project AGENTS Writer
##### Suggested Sections
Keep content to rules, constraints, and who decides.
- Concept: what the project is and why it exists (kind of project, e.g. software, event, research, creative work; goals, scope, explicit non-goals)
- Members: who takes part and in what capacity (roles, responsibilities, skill sets, whom to ask about what, handoff and approval rules)
- Design: how the concept takes concrete form (design docs, style guides, asset locations)
- Engineering: the technical means of building it (tools, standards, environments, technical constraints)
- Business: the commercial and legal frame (budget, contracts, legal constraints, confidentiality, decision authority)
- Marketing: how the project reaches its audience (marketing plan, market research, voice, channels, what needs approval before publishing)
- Production: how the work gets made and finished (workflows, tools, quality checks, naming and versioning rules)
- Operations: what follows completion (release, maintenance, steps for each recurring task)
- Logistics: practical support for the team so work can happen (supplies, venues, travel, who books or approves)
- Timeline: when things happen (milestones, deadlines, current phase, date format, which deadline wins on conflict)
Split content by topic, never by type: a tool or resource link tied to production sits under Production, not in a separate links section.
### Create Project AGENTS
1. ground the file in the project's own material and the conversation; write only what they support
2. keep the root file generic; add a scoped file only where a subfolder's rules differ
3. create `AGENTS.md` per [Project AGENTS Writer](#project-agents-writer), formatted per [Style Guide Markdown Format](#style-guide-markdown-format)