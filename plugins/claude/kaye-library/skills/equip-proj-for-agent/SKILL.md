---
name: equip-proj-for-agent
description: 'Equips project for AI agents: writes & maintains its `AGENTS.md`'
when_to_use: 'Setting up or updating agent instructions for a generic project. Triggers: "equip project for agent", "make project AI-ready"'
metadata:
  version: 1.6.2
---

## Project Context Engineering
- For Agents:
  - Agent File: `AGENTS.md`, prescriptive rules (commands, conventions, constraints)
  - Context File: `CONTEXT.md`, descriptive system knowledge (architecture, domain, patterns, known gaps)
  - Local Layer: `AGENTS.local.md`, `CONTEXT.local.md`, personal and private, read over its file
- For Users First: agents may read too
  - Readme File: `README.md`, landing page (what the project is, how to start, where next); always at the project root
  - Doc Files: `docs/`, in-depth topic documents beyond the readme
- Project-Specific Skill: reusable instructions for a task only this project performs
The root agent and context files hold project-wide information. A scoped agent or context file is optional: it sits in a subfolder and holds only what is specific to that folder and beneath.
Explore before you assume, at the opening of a conversation and whenever a gap appears: read the agent file, then the context file, each with its local layer over it, then only the doc files the topic names.
Read the layers from the root down to the folder you are editing, each scoped file over its parent. On a conflict, the closest file wins; the user's word in chat overrides every file.
When no file answers, open the actual source, config, or schema and verify what is checkable.
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