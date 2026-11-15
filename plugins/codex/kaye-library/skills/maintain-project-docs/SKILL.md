---
name: maintain-project-docs
description: Updates existing project `docs/` files against what changed, editing in place
when_to_use: 'Triggers: "update the docs", "the docs are out of date", changed decision, tool, or process'
metadata:
  version: 1.4.0
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
## doc writer
Apply these rules to the topic documents under `docs/`, formatting them per [Style Guide Markdown Format](#style-guide-markdown-format) and writing them per [Style Guide Good Writing](#style-guide-good-writing).
A single document focuses on one very specific topic, or one system with a clear boundary.
### Project Doc Writer
Draw from the project's own material, and verify every claim against it.
### Maintain Project Docs
You work from a **change set**: what the conversation and the project have altered since the docs were written. A document the change set never reaches is left exactly as it reads.
1. edit in place: update what the change set moved, fix references it broke, cut what it made stale, duplicated, or unsupported
2. leave each document's audience, scope, and sound wording alone
3. verify facts against the project; keep links current
4. create a document only where the change set requires it
5. follow [Project Doc Writer](#project-doc-writer), [Style Guide Markdown Format](#style-guide-markdown-format), and [Style Guide Good Writing](#style-guide-good-writing), then return a brief summary listing changed files