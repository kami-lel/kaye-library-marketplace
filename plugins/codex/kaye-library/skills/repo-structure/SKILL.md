---
name: repo-structure
description: Defines a standard, language-agnostic project/repository layout — naming conventions and placement for top-level documentation files and source, build, docs, test, and tooling folders.
when_to_use: 'Use when scaffolding a new repo, organizing an existing one, or deciding where a file or folder belongs. Triggers: "set up project structure," "where should this go," naming a standard doc or directory.'
metadata:
  version: 1.6.1
---

## Repository Structure
A repository keeps its readme, agent, context, and doc files as set out in [Project Context Engineering](#project-context-engineering), with one addition: local layers are machine-specific, gitignored, and never committed.
Place the following at the **top level** of the repository when applicable, named consistently across projects:
- `CHANGELOG.md`: full version history; each release is documented here
- `CREDITS.md`: third-party assets and libraries, with source, author, and license; optionally contributors and acknowledgments
- `DEVLOG.md`: development journal, decisions, and progress notes
- `src/` or package-name: primary source code folder
- `bin/`: compiled binaries or executable entry-point scripts
- `examples/`: standalone usage examples and demos
- `scripts/`: utility and maintenance scripts not part of the main codebase
- `tests/`: test suite, kept separate from source code
- `tools/`: project-specific developer tooling, distinct from `scripts/`