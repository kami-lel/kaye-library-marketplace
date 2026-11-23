---
name: style-markdown-endnotes
description: Attaches a footnote-style identifier link inline and collects every definition in an endnotes block at the file's end.
when_to_use: When a link needs a compact inline marker with full references at the document's end.
metadata:
  version: 1.6.0
---

### Markdown Endnotes
- attach each link to a footnote marker `[^id]`, where `id` is a 1~3 word identifier drawn from the link's subject
- do not define the footnote inline; collect every definition under a single `<!-- Endnotes -->` marker at the document's end
- order endnote definitions by first appearance in the text
- keep each definition to one line: the marker and its link or description
##### Example
```md
See the style guide[^style-guide] for format rules.

...

<!-- Endnotes -->

[^style-guide]: https://example.com/style-guide
```