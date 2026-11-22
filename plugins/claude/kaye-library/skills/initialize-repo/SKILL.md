---
name: initialize-repo
description: Bootstraps a repository's entire baseline documentation set in one pass — `README.md`, `CHANGELOG.md`, `AGENTS.md`, `CONTEXT.md`, and `docs/` — from a single repository inspection, splitting content by purpose with no duplication and skipping files that already exist.
when_to_use: When a bare repo needs its documentation scaffolded all at once — "set up docs," "set up this project/repo," "document this project," "create the docs from scratch." Not for updating or fixing existing docs.
metadata:
  version: 1.5.1
---

## Style Guide Good Writing
- Correct spelling, grammar, punctuation, sentence structure, and verb tense errors.
- Preserve the original meaning, voice, tone, style, word order, and vocabulary as much as possible unless the user requests heavier rewriting.
- Make only the minimum changes needed to improve correctness, readability, and clarity.
- Ensure the revised text is clear, polite, and free of language errors.
- Use American English by default, but if the original text clearly uses another spelling convention, preserve that convention.
- Expand uncommon abbreviations only when doing so improves clarity.
- Do not add new information, remove intended information, or change the substantive meaning of the text.
- Avoid generic filler when details are unavailable
- Avoid dense prose, generic filler, and unnecessary complexity
## Initialize Repository
Bootstrap a repository's baseline documentation from nothing, in one pass. Write everything per [Style Guide Markdown Format](#style-guide-markdown-format) and [Style Guide Good Writing](#style-guide-good-writing).
#### Instructions
- inspect the repository once — layout, configs, manifests, scripts, tests — and take the rest from the conversation. Reuse those findings across every step below
- run each create skill in order, skipping any whose target file already exists:
  1. [Create README](#create-readme) → `README.md`, per [Repository README Writer](#repository-readme-writer)
  2. [Create CHANGELOG](#create-changelog) → `CHANGELOG.md`, per [Repository CHANGELOG Writer](#repository-changelog-writer)
  3. [Create Repository AGENTS](#create-repository-agents) → `AGENTS.md`, per [Repository AGENTS Writer](#repository-agents-writer)
  4. write `CONTEXT.md` directly, per [Repository CONTEXT Writer](#repository-context-writer)
  5. [Create Repository Docs](#create-repository-docs) → files under `docs/`
- split by purpose and never duplicate: human onboarding → README, release history → CHANGELOG, agent behavior → AGENTS, system knowledge → CONTEXT, topic deep-dives → `docs/`
- write a file or section only where project information supports it
#### Output
Create the documentation files at their standard locations.
Return a brief summary listing every file created.
### {[Claude:Skill] Usage}
Invoke `create-readme`, `create-changelog`, `create-repo-agents`, and `create-repo-docs` skills via `Skill` tool.