---
name: equip-proj-for-agent
description: 'Equips project for AI agents: writes & maintains its `AGENTS.md`'
when_to_use: 'Setting up or updating agent instructions for a generic project. Triggers: "equip project for agent", "make project AI-ready"'
metadata:
  version: 1.5.1
---

## Project Context Engineering
- For Agents:
  - Agent File: `AGENTS.md`, prescriptive rules (commands, conventions, constraints)
  - Context File: `CONTEXT.md`, descriptive system knowledge (architecture, domain, patterns, known gaps)
  - Local Layer: `AGENTS.local.md`, `CONTEXT.local.md`, personal and private, over its file
- For Users First: agents may read too
  - Readme File: `README.md`, landing page (what the project is, how to start, where next); must sit at project root
  - Doc Files: `docs/`, in-depth topic documents beyond the readme
- Project-Specific Skill: reusable instructions for a task only this project performs
A scoped agent/context file is optional: it sits in a subfolder and covers only that folder and beneath with specific information; the root agent/context file holds generic, project-wide information.
Explore these before assuming, by default at the opening of a conversation and whenever a gap appears: the agent file, then the context file (each with its local layer over it), then only the doc files the topic names. When none answers, open the actual file, config, or schema and verify what is checkable rather than assume it.
#### Folder Structure Example
```text
ExampleProject/
├── .claude/
│   └── skills/
│       └── write-release-note/
│           └── SKILL.md
├── README.md
├── AGENTS.md
├── CONTEXT.md
├── CREDITS.md
├── DEVLOG.md
├── docs/
│   └── setup-guide.md
└── Frontend/
    ├── AGENTS.md
    ├── AGENTS.local.md
    └── CONTEXT.md
```
## Equip Project for Agent
Task: create or maintain the project's `AGENTS.md` per [Project AGENTS Writer](#project-agents-writer).
### {[Claude:Skill] Usage}
Invoke `proj-agents-writer` skill via `Skill` tool, asking it to create or maintain the project's `AGENTS.md`.