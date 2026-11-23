---
name: create-credits
description: Bootstraps a `CREDITS.md` for a repository that has none, inventorying every third-party asset, font, sound, and bundled library it ships, with each one's source, author, and license.
when_to_use: Trigger on "create a credits file", "credit our assets", "list the third-party assets", or a repository shipping third-party material with no `CREDITS.md`.
metadata:
  version: 1.6.0
---

## Style Guide Briefness Style
- write in **newspaper headlinese**, prioritize brevity over grammar
- use present for current, infinitive for planned
- omit articles (a, an, the) and helper verbs, use strong nouns, verbs
- compress with punctuation: colon, dash, comma, otherwise minimize, no terminal periods
- use numerals (use 2, not two), symbols, common abbreviations when unambiguous
- prefer active voice
- keep sentences short, direct, drop filler
Aggressively replace the full form with its shorthand:
- vs.:against
- &:and
- ~:and the others (eg a, b, ~)
- ~~:and the others (eg a, b, ~~; use when ~ is ambiguous)
- ⇐:because,caused by,result of
- ←:become/change/transform from
- →:become/change/transform into
- b/t:between
- cf.:confer,compare
- ↓:decrease,decrement
- 〃:ditto,repetitive as above/before
- e.g.:example
- iff:if and only if
- re:in the matter of,concerning,regarding
- ↑:increase,increment
- misc.:miscellaneous
- n/a:not applicable
- №:number
- \:of
- /:or
- ~:range (eg 1~5, a~f, ii~iv)
- 〃:same as cell above
- i.e.:that is,in other words
- ⇒:therefore,causing,resulting
- ※:which see,reference to
- w/:with
- w/i:within
- w/o:without
## Style Guide Good Writing
- Correct spelling, grammar, punctuation, sentence structure, and verb tense errors.
- Preserve the original meaning, voice, tone, style, word order, and vocabulary as much as possible unless the user requests heavier rewriting.
- Make only the minimum changes needed to improve correctness, readability, and clarity.
- Ensure the revised text is clear, polite, and free of language errors.
- Use American English by default, but if the original text clearly uses another spelling convention, preserve that convention.
- Expand uncommon abbreviations only when doing so improves clarity.
- Do not add new information, remove intended information, or change the substantive meaning of the text.
- Avoid generic filler when details are unavailable
- Avoid dense prose, generic filler, and unnecessary complexity
## Repository CREDITS Writer
You write and maintain a repository's `CREDITS.md`: the record of every third-party asset and library the project ships, with the author and license each one demands, and, where the team wants them, the people who made the project and those who helped it. It serves the creators being credited, anyone checking that the project may use what it ships, and the team deciding whether an asset can stay. A credit nobody can trace to a file, a source, and a license is not a credit.
#### CREDITS Title & Preface
```markdown
# Example Repository CREDITS

The people behind Example Repository, and the third-party assets it uses.
```
Replace `Example Repository` with the real repository name. When the file carries no Contributors section, the preface reads `Third-party assets used in Example Repository.`
#### Sections
One `##` section each, holding only those the project has, in this order:
- Contributors: optional; the people and teams who made the project, per [Contributors and Acknowledgments](#contributors-and-acknowledgments)
- Visual Assets: one section each for Sprites, Textures, Models, and Animations
- Fonts: typefaces, with the font files and engine font assets made from them
- Audio: one section each for Music and Sound Effects
- Code: vendored or copied source, and bundled libraries whose license asks for credit
- Acknowledgments: optional; help that shipped no file, per [Contributors and Acknowledgments](#contributors-and-acknowledgments)
Dependencies a package manager installs stay out, unless their license asks for credit in the shipped product.
#### Asset Table
Each asset section is one table, one row per asset, or per set of assets sharing one source:
| Column | Holds |
|---|---|
| Asset | path in the repository, in backticks; for a set, the folder path, with its files and the role each plays in parentheses; any change made to the original |
| Source | asset title linked to the page it came from, with the platform in parentheses when the title does not name it; attribution text the license requires, quoted exactly |
| Author | the creator as the source credits them; several people each with their role in parentheses, ie original, edit |
| License | license name linked to its canonical text; a custom or store license in plain words, with any condition that limits use, ie personal use only |
Escape a `|` inside a cell as `\|`.
<credits-example>
| Asset | Source | Author | License |
| --- | --- | --- | --- |
| `Assets/Sprites/Coin/` (`coin-spin-01.png` to `coin-spin-08.png`, the pickup animation; recolored gold) | [Coin Pack](https://example.com/coin-pack) (Example Asset Site) | Example Artist (original), Example Editor (recolor) | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) |
| `Assets/Fonts/ExampleSans/` (`ExampleSans-Bold.ttf`, the UI font, its `OFL.txt`, and the engine font asset made from it) | [Example Sans](https://example.com/example-sans) | Example Type Foundry | [SIL Open Font License 1.1](https://openfontlicense.org) |
</credits-example>
<credits-counter-example>
[Coin Pack](https://example.com/coin-pack) by Example Artist

[Background Music](https://example.com/track)
</credits-counter-example>
The counter-example names no file and no license, and its second line no author: a reader cannot tell what each line covers, or whether the use is allowed.
#### Contributors and Acknowledgments
Both are optional; write them only when the team wants people credited.
- Contributors: one item per person or team, labeled with the name as they wish to be credited, followed by their role, ie programming, art, music; a guest contributor's role names what they made
- Acknowledgments: one item per person or group who helped without shipping a file, ie advisors, playtesters, mentors, references, labeled with the name or group and followed by what the help was
- Names Only: credit a person by name and role; add no contact details, accounts, or links unless that person asks for them
<contributors-example>
```markdown
## Contributors

- Example Lead: programming, systems design
- Example Artist: art, animation
- Example Composer: music, exploration theme (guest)

## Acknowledgments

- Example Playtest Group: the 02026-10-20 playtest
- Example Advisor: feedback at the alpha review
```
</contributors-example>
#### Quality Expectations
- complete: every third-party file the repository ships has a row, and every row's path exists
- traceable: every source a working link, every license named
- honest: a field nobody can confirm reads `unknown`, never a guess
- faithful to the license: the attribution wording, modification notes, and use conditions it requires all present
- formatted per [Style Guide Markdown Format](#style-guide-markdown-format), cells kept terse per [Style Guide Briefness Style](#style-guide-briefness-style), prose written per [Style Guide Good Writing](#style-guide-good-writing)
## Create CREDITS
1. inventory the third-party material the repository ships: asset folders, fonts, audio, vendored code, bundled libraries
2. read the license, readme, and attribution files shipped beside each, and any credits already in the README, DEVLOG, or build notes
3. take sources, authors, and licenses the repository has not captured from the conversation, and, when the user wants them, the contributors with their roles and the acknowledgments
4. write one row per asset under its section, marking every field nobody can confirm `unknown`
5. create `CREDITS.md` at the project root, for a repository that has none, per [Repository CREDITS Writer](#repository-credits-writer), [Style Guide Markdown Format](#style-guide-markdown-format), and [Style Guide Good Writing](#style-guide-good-writing), then return a brief summary listing every `unknown` field