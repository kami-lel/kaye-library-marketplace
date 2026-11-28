---
name: maintenance-before-compact
description: Logs a session's durable changes before context compaction — recording them in `CHANGELOG.md` and syncing `AGENTS.md` and `CONTEXT.md` — identifying the change set once from the conversation, working diffs, and existing `[Unreleased]` entries.
when_to_use: Trigger on "before compact", "context is about to compact", "save this session's progress", or "log the session's changes before the context fills".
metadata:
  version: 1.6.1
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
## Maintenance Before Compact
Before context is compacted, capture this session's durable changes so nothing is lost — log them and update the agent-facing docs. Format per [Style Guide Markdown Format](#style-guide-markdown-format) and write per [Style Guide Good Writing](#style-guide-good-writing).
#### Instructions
- identify the session's changes once, from the conversation, working diffs, and existing `[Unreleased]` entries, then reuse that set below
- [Maintain CHANGELOG](#maintain-changelog) → record those changes; the unreleased-only and deduplication rules come from that skill
- [Maintain Repository AGENTS](#maintain-repository-agents) → update for any command, convention, or constraint the session moved, in the layer nearest the changed files
- update the `CONTEXT.md` nearest the changed files directly for any architecture the session moved, per [Repository CONTEXT Writer](#repository-context-writer)
- skip a step the session gives nothing relevant to
#### Output
Update the affected files in place, leaving unrelated files untouched.