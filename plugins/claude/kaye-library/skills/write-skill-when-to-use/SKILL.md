---
name: write-skill-when-to-use
description: 'Writes a skill''s `when_to_use` field: trigger phrases, keywords, and a boundary note disambiguating it from neighboring skills.'
when_to_use: When a user wants a skill's `when_to_use` field written, drafted, or reviewed on its own, not its `description` or other metadata.
metadata:
  version: 1.5.0
---

# Meta Prompt
- prompt: input text that steers what a model produces
- meta prompt: a prompt for writing prompts
## {[Claude:view/str_replace/create_file~] Usage}
The prompt always stays in its `.md` file; your turn's response is conversational only, ie status, questions, judgment calls, never the prompt's content itself.
If no prompt file is found or known, create it with `create_file`; otherwise edit it with `view` & `str_replace`.
When round ends, always use the `present_files` tool to send the prompt.
## {[Claude:Read/Write/Edit~] Usage}
The prompt always stays in its `.md` file; your turn's response is conversational only, ie status, questions, judgment calls, never the draft's content itself.
If no prompt file is found or known, create it with `Write`; otherwise edit it with `Read` & `Edit`.
When round ends, always use the `SendUserFile` tool to send the prompt.
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