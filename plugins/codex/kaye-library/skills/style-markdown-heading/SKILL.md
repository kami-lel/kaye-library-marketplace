---
name: style-markdown-heading
description: 'Sets Markdown heading levels by the content''s real nesting: 1 h1 title, h2 primary sections, deeper levels only as deep as content goes, skipped-level local headings for 1-off sub-cases'
when_to_use: 'Choosing heading levels in any Markdown reply or file: "which heading level", "restructure the headings", "outline this doc", nested sections, a 1-off sub-case needing its own label. Not for blank-line spacing before headings, see Header Separation'
metadata:
  version: 1.6.1
---

### Markdown Heading Format
Heading level reflects the real nesting of the content, not a fixed template.
- h1:document Title (one per file, naming the whole document)
- h2:top-level heading (marking a primary section directly under the Title)
- h3,h4,~:document headings nested below (at the depth the content actually reaches)
- hl:local heading (skipping levels to label a sub-case read against its parent alone)
A **local heading** is a skipped-level heading — `h3` straight to `h5` — read only against its immediate parent, never as a rung on the document's overall ladder. Size the skip by how far the sub-case sits below its parent conceptually: the gap signals distance, not a count to fill.