---
name: amanuensis-chicago-note
description: 'Generates Chicago Manual of Style notes-bibliography footnotes: kebab-case slugged markers, source-template citations, annotated notes, collected as native Markdown footnotes at file end'
when_to_use: 'Trigger on "add footnote", "cite this", "format as CMS footnote", `[^slug]` markers, or inline citation requests needing notes-bibliography form. Boundary: footnote markers and end-of-file definitions only, not bibliography-list entries'
metadata:
  version: 1.4.1
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
### Chicago Note
- label every marker with a kebab-case slug, never a bare number — `[^smith-tariff-data]`, `[^yt-kiln-firing]`, `[^why-1972-cutoff]`
- keep each slug to Two or Three Words, lowercase, hyphen-separated, drawn from the Author Surname, site name, or subject; add a distinguishing word when one source is cited for several separate points
- keep slugs Unique within a file; one slug maps to exactly one definition
- place the marker immediately after the closing punctuation, no space before it, and never two markers side by side on the same sentence
- reuse the original slug when re-citing a source at the same page; append a page suffix for a different page — `[^smith-wealth-p204]`
See [Markdown Footnotes](#markdown-footnotes) for definition placement.
##### Source Templates
- website — `[^bls-cpi-method]: "Page Title," Organization, Month D, Year, https://...`
- online journal article — `[^chen-supply-chain]: Firstname Lastname, "Article Title," *Journal Name* 12, no. 3 (Year): p. 99, https://doi.org/...`
- database entry — `[^oed-tariff]: "Entry Title," *Database Name*, Month D, Year, https://...`
- YouTube video — `[^yt-kiln-firing]: Channel Name, "Video Title," YouTube video, 12:34, Month D, Year, https://...`
- book — `[^smith-wealth]: Firstname Lastname, *Title of Book* (Place: Publisher, Year), p. 99.`
- repeat reference — use the shortened form `Lastname, *Short Title*, p. 99.`, never `Ibid.`
- multiple sources for one claim — gather them into a single note, separated by semicolons, in the order they support the claim