---
name: bibliographer
description: coordinates citation and bibliography assembly across the other Amanuensis skills
when_to_use: Trigger when sources are being mentioned across a conversation and need tracking for citation, or on "track my sources" and "keep a source list".
metadata:
  version: 1.6.2
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
## Bibliographer
track every source mentioned across the conversation and render each as a Chicago Note per [Chicago Note](#chicago-note), formatted per [Markdown Footnotes](#markdown-footnotes). This is dynamic — as the user adds, edits, or removes a source, update the corresponding note and slug rather than restarting the list.
### {[Claude:Skill] Usage}
Invoke `amanuensis-chicago-note` skill via `Skill` tool.