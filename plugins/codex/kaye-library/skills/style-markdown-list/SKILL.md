---
name: style-markdown-list
description: 'Formats Markdown lists and table cells: dash bullets, items in Commentary Case, optional Title Case colon labels with key words bolded, numbering only for intrinsic order, nesting for composite items, shorthand symbols for boolean and n/a cells'
when_to_use: 'Any bullet list, term/definition pair, key-value label, or table in a reply or Markdown file: "make this a list", "bullet these", "label each item", "add a table". Not for prose paragraphs'
metadata:
  version: 1.6.1
---

### List Format
Use `-` (dash) for bullet point lists
Item rules:
- Case: write each item in [Commentary Case](#letter-case-commentary-case)
- Label: when an item defines a term or pairs a key with a description, lead with a [*Title Case*](#letter-case-title-case) label and a colon, no space before, one after; the description follows in Commentary Case
- Emphasis: leave labels plain; bold 1~2 key words inside each item's description; bold a label only where the item must not be missed; never italicize a label; use backticks only for identifiers, flags, paths, and literals
- Consistency: label every item or none
- Numbering: number a list only when order is intrinsic, such as algorithm steps, frames, or setup procedures; categories stay dash-bulleted
- Nesting: carry a composite item as one parent label with indented sub-bullets, never as flattened sibling lines
<labeled-list-example>
- First Label: plain label, the **key words** of the description bolded
- **Second Label**: bolded because it must not be missed, with a **second key word** in the description
- `--third-flag`: backticks for an identifier, not for emphasis
</labeled-list-example>
In a table cell, aggressively replace the boolean/not-applicable value with its listed entry:
- ❌:no;false
- ➖:not applicable
- ✔️:yes;true
- 〃:same as cell above
- ☚:same as cell to left
----
A section with many lists commonly uses this form: each list opens with an intro line ending in a colon, then a blank line, the items, and a blank line after.
<list-format-example>
the fruit in the basket:

- apple
- pear, ripe enough to eat today

the tools on the bench:

- hammer
- saw
</list-format-example>