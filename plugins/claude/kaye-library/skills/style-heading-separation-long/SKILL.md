---
name: style-heading-separation-long
description: Sets wide blank-line spacing before Markdown headers, for long files
when_to_use: Long, many-section Markdown documents needing generous separation between sections
metadata:
  version: 1.5.1
---

# Style Guide
## Style Guide Markdown Format
Please style your responses using *Github Flavored Markdown*. Avoid mentioning markdown or styling in your response.
Follow these guidelines in every conversation:
- Use **double asterisks** (`**`) for **bold** text on **key words**: the term a passage defines, the command or action to run, a warning, a decision, a result. In prose and documents, bold generously: a reader skimming only the bold should recover the gist
- Employ *single asterisks* (`*`) for *italics* to reference titles of books, movies, games, and secondary important information
- do not use underscores (`_`) for bold/italics formatting.
### Header Separation
You must add *empty lines* before each section header, with the **number of empty lines determined by the header level** provided in the table.
Note: Do not include the text inside parentheses `()`, these are *instructions* showing where to insert empty lines.
#### Long File
| Level | MD Header                       | Empty Line Before |
|-------|---------------------------------|-------------------|
| 2     | `## Level 2 Header Example`     | 34                |
| 3     | `### Level 3 Header Example`    | 13                |
| 4     | `#### Level 4 Header Example`   | 5                 |
| 5     | `##### Level 5 Header Example`  | 3                 |
| 6     | `###### Level 6 Header Example` | 2                 |
    <header-separation-long-file-example>
    (...)
    Brief project description.
    (34 EMPTY LINES BEFORE LEVEL 2 HEADER)
    ### Installation
    Step-by-step instructions.
    (13 EMPTY LINES BEFORE LEVEL 3 HEADER)
    #### Usage
    (...)
    </header-separation-long-file-example>