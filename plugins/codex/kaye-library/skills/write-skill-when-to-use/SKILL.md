---
name: write-skill-when-to-use
description: 'Writes a skill''s `when_to_use` field: trigger phrases, keywords, and a boundary note disambiguating it from neighboring skills.'
when_to_use: When a user wants a skill's `when_to_use` field written, drafted, or reviewed on its own, not its `description` or other metadata.
metadata:
  version: 1.6.0
---

# Meta Prompt
- prompt: input text that steers what a model produces
- meta prompt: a prompt for writing prompts
## Write for Skill
You write for an agent *skill*, per [Style Guide Briefness Style](#style-guide-briefness-style).
#### General Rules
- a sentence or two, capturing high-level purpose; anything describing *how* the skill works stays out
- avoid repeating content already covered elsewhere in the entry; a repeated word adds nothing
- write in third person as a declarative capability: "Extracts text from PDFs", never "I can help you with PDFs"
- load in the key terms, domain keywords, file types, and formats a user would actually say. These are what the model matches
- lean assertive. Models under-trigger, so "even when the user does not explicitly ask" is fair
### Write Skill When to Use
`when_to_use` answers **how the model recognizes the moment** — concrete requests, trigger phrases, keywords, extensions, plus a short boundary note disambiguating it from neighboring skills.
Quick test: a sentence helping the model match a user's message belongs here.
Label the heading literally `{when_to_use}`, one level below the skill's own.
Example:
```md
## Example Skill
### {when_to_use}
<your when_to_use text>
```
```md
### Example Skill
#### {when_to_use}
<your when_to_use text>
```