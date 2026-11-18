---
name: style-markdown-file-assets
description: Places a Markdown file's images and other assets in a sibling `<name>-assets/` folder, eg `CHANGELOG.md` → `CHANGELOG-assets/`, linked by a relative `./` path.
when_to_use: 'Adding an image, screenshot, diagram, or attachment to a `.md` file, or deciding where its assets live: "add a screenshot to the README", "embed this image in the docs", any `![…](…)` link, even when no folder is named. Not for links to external pages.'
metadata:
  version: 1.5.0
---

### Markdown File Assets
Keep a Markdown file's assets, mostly images, in a sibling folder named for it, so the file and its assets move together.
- Folder: base name plus `-assets`, case kept, holding that file's assets only: `CHANGELOG.md` → `CHANGELOG-assets/`
- Link: a relative path opening with `./`
- Name: in an asset's name, a space or a character illegal in a path or URL becomes `_`, so the link needs no escaping
```md
![Install dialog](./setup-guide-assets/install-dialog.png)
```
#### {avoid}
A shared `images/` folder, absolute paths, or repository URLs, which break once the file moves.