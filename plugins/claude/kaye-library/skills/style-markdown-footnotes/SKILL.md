---
name: style-markdown-footnotes
description: Attaches a Markdown footnote to each link, keeping the footnote's definition directly beside its reference.
when_to_use: When a link needs an inline note kept close to the text, not batched at the document's end.
metadata:
  version: 1.5.0
---

### Markdown Footnotes
- attach each link to a footnote marker `[^id]`, where `id` is a 1~3 word identifier drawn from the link's subject
- place the footnote definition `[^id]: ...` immediately after the line or paragraph carrying the link
- keep the footnote text to a single short line naming what the link is
- reuse an identifier only for the same link; each distinct link gets its own
##### Example
```md
See the style guide[^style-guide] for format rules.

[^style-guide]: https://example.com/style-guide
```