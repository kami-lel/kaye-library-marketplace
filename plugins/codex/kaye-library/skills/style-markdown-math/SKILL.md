---
name: style-markdown-math
description: 'Renders math in LaTeX: inline `$…$`, block `$$…$$`, each formula glossed symbol by symbol beneath it'
when_to_use: 'Any equation, formula, variable, or calculation in a reply or Markdown file, even a short inline expression: "write the formula", "show the math", "derive", "LaTeX". Not for code that computes the values'
metadata:
  version: 1.6.0
---

### Math Formatting
Use LaTeX for all mathematical expressions. Do not write math in plain text.
- Inline math: use single dollar signs — `$a = b + c$`
- Block math: use double dollar signs on separate lines:
$$
a^2 + b^2 = c^2
$$
Gloss a formula symbol by symbol: one short bullet per symbol beneath it, never one combined paragraph.