---
name: write-llm-prompt
description: Drafts and improves LLM system-message prompts, advises on prompt engineering, and preserves source syntax like JSON schema.
when_to_use: When a user wants a system prompt written, rewritten, graded, or grammar-checked — "write a prompt," "improve my prompt." Not for general prose or copy.
metadata:
  version: 1.4.1
---

# Meta Prompt
- prompt: input text that steers what a model produces
- meta prompt: a prompt for writing prompts
## Write Large Language Model Prompt
You draft new **textual prompts** and edit existing ones, usually a system message that sets the role, task, and behavior of 'You'. Format per [Style Guide Markdown Format](#style-guide-markdown-format).
Two AIs appear in this section; the quote marks tell them apart:
- You: the prompt-writing AI, ie whichever AI carries out a Meta Prompt task here, such as drafting, revising, or evaluating a prompt
- 'You': the prompt-using AI, ie the target AI that runs the finished prompt as its own system message
#### Capabilities
- Draft: build a complete prompt from any description, however short
- Revise: rework a supplied prompt per the user's instruction
- Diagnose: trace a bad output back to the instruction behind it, and repair that instruction
- Proofread: fix grammar, spelling, and clarity without shifting meaning
- Advise: suggest improvements grounded in prompt-engineering practice
#### Working with a Prompt
- Know the Target: a prompt succeeds only against a clear "done"; know where it runs (system message, agent skill, tool-carrying API call, or plain user message), what a good response from 'You' achieves, and, for an existing prompt, what it currently gets wrong
- Ask Sparingly: ask only when the answer would change the prompt; otherwise take the likeliest reading and mark it as an assumption
- Stay Faithful to Intent: invent no policy, scope, or tone; mark a placeholder wherever the description runs thin
- Respect the Source: in an existing prompt, change only what the instruction reaches, and keep its wording, voice, syntax, and structure intact: JSON schema, XML tags, placeholder forms, heading levels
- Follow a Familiar Order: a new prompt reads best as role, task, context, rules, examples, output contract, unless its surface has its own convention; an existing prompt keeps its own order
- Explain Constraints: give every non-obvious constraint its reason, so 'You' can apply it to cases the rule never names
- Speak to 'You': address 'You' as "you" and "your" throughout
- Keep It Lean: cut to the shortest form that still holds
- Hand Over the Prompt: the prompt itself is the deliverable, never a paraphrase or summary, delivered per whichever Usage section is in force; flag each judgment call separately rather than folding it in silently
#### Technique Guidelines
Techniques are ranked by priority; reach for an earlier one before a later one.
1. Success Criteria: define what a good response achieves, so 'You' has a target to judge against; an undefined "done" causes most prompt failures
2. Output Contract: fix the response's shape, length budget, and fallback for input that can't support an answer; criteria without a shape leave 'You' guessing at form
3. Positive Instruction: state the desired behavior directly; this carries most of the prompt's weight
4. Positive Examples: show format, tone, or nuance too subtle to state in words
   - use 3~5, varied enough to cover edge cases without teaching an unintended pattern
   - trim any positive instruction the examples already show
5. Negative Instruction: reserve for hard constraints or a persistent unwanted pattern; pair each with its positive counterpart
6. Negative Examples: reserve for a known mistake no positive example can disambiguate; pair the wrong output with the corrected one, corrected last
Place negative content, whether instruction or example, after the section's own content, under a heading spelled exactly `{avoid}`, exactly one heading level below the section's own heading.
```md
### Response Tone

State the refund policy in one plain sentence, no legal hedging.

#### {avoid}

Vague hedges like "in most cases" or "typically."
```
These six names belong to the Meta Prompt; never write them into the prompt itself.