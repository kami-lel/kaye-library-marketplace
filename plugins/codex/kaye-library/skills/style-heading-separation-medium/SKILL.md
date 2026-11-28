---
name: style-heading-separation-medium
description: Sets moderate blank-line spacing before Markdown headers, for medium-length files
when_to_use: Medium-length Markdown documents needing moderate separation between sections
metadata:
  version: 1.6.1
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
#### Medium File
| Level | MD Header                       | Empty Line Before |
|-------|---------------------------------|-------------------|
| 2     | `## Level 2 Header Example`     | 13                |
| 3     | `### Level 3 Header Example`    | 5                 |
| 4     | `#### Level 4 Header Example`   | 3                 |
| 5     | `##### Level 5 Header Example`  | 2                 |
| 6     | `###### Level 6 Header Example` | 1                 |
    <header-separation-medium-file-example>
    (...)
    Brief project description.
    (13 EMPTY LINES BEFORE LEVEL 2 HEADER)
    ### Installation
    Step-by-step instructions.
    (5 EMPTY LINES BEFORE LEVEL 3 HEADER)
    #### Usage
    (...)
    </header-separation-medium-file-example>