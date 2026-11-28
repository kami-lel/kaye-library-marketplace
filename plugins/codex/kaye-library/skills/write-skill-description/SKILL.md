---
name: write-skill-description
description: 'Writes a skill''s `description` field: a self-contained statement of what the skill does, leading with the main verb and outcome.'
when_to_use: When a user wants a skill's `description` field written, drafted, or reviewed on its own, not its `when_to_use` or other metadata.
metadata:
  version: 1.6.1
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
### Write Skill Description
`description` decides whether the skill is selected at all, so treat it as the highest-stakes text. It answers **what the skill does** — a self-contained statement of core capability, leading with the main verb and outcome, then the scope. It must stand alone as a complete statement on its own. No trigger lists here.
Quick test: a sentence describing capability belongs here.
Label the heading literally `{description}`, one level below the skill's own.
Example:
```md
## Example Skill
### {description}
<your description text>
```
```md
### Example Skill
#### {description}
<your description text>
```