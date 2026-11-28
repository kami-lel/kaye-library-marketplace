---
name: amanuensis-chicago-bibliography
description: 'Generates Chicago Manual of Style bibliography entries: source-template citation lines and annotated entries for a Works Cited or reference list'
when_to_use: 'Trigger on "add to bibliography", "list sources", "format as CMS bibliography", "Bibliography" requests, or annotated-bibliography requests. Boundary: bibliography-list entries only, not inline footnote markers'
metadata:
  version: 1.6.2
---

# Amanuensis
## Chicago Citation
You write citations in the *Chicago Manual of Style* (hereafter CMS) notes-bibliography system, producing footnote entries as native Markdown footnotes within a document, and, on request, a full citation paragraph combining footnotes and bibliography as an appendix or as the entirety of the next response, drawing all bibliographic detail from the user's input and the chat history.
#### Citation Form
- italicize book, journal, site, and database titles with single asterisks; put article, page, chapter, and video titles in "double quotation marks"
- end every note with a period
- give one date only, preferring the Publication Date, else `last modified Month D, Year`, else `accessed Month D, Year`
- write the URL bare and in full; never a markdown link, never inside angle brackets, never shortened, truncated, or carrying Tracking Parameters
- consult the *Chicago Manual of Style* directly for any source type not covered in the templates below
#### Page Numbers
Override the Chicago rules on numerals and dashes. Always prefix page references
- single page: `p. 99`
- page range: `pp. 99~104`, joined by a Tilde with no surrounding spaces, never an en dash or hyphen
- discontinuous pages: `pp. 5, 13, 15`, comma-separated in Ascending Order
#### Annotation
A footnote or a bibliography entry may carry commentary instead of, or alongside, a citation. Formatting for each form is given under its own heading below
- keep annotation prose in Full Sentences, distinct in voice from the citation string
- multi-paragraph annotation — break with a blank line and indent the following paragraph by four spaces
### Chicago Bibliography
a bibliography is a single alphabetical list of every source consulted, appearing once at the end of the document, with each entry giving Full Publication Details in a fixed template per source type.
##### Source Templates
- book — `Lastname, Firstname. *Title of Book*. Place: Publisher, Year.`
- online journal article — `Lastname, Firstname. "Article Title." *Journal Name* 12, no. 3 (Year): pp. 95~99. https://doi.org/....`
- website — `"Page Title." Organization, Month D, Year. https://....`
- database entry — `"Entry Title." *Database Name*, Month D, Year. https://....`
- YouTube video — `Channel Name. "Video Title." YouTube video, 12:34. Month D, Year. https://....`
##### Placement
- collect every entry under a heading titled `Bibliography`, at the level appropriate to the document, at the **end of file**
- list entries as a flat bullet list, one entry per line
- order entries alphabetically by the first element of the citation — Author Surname when present, otherwise the first word of the title, ignoring *A*, *An*, and *The*