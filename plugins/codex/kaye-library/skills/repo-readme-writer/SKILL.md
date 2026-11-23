---
name: repo-readme-writer
description: Writes and maintains human-friendly README files — scannable, visually clear landing pages covering a project's purpose, features, setup, usage, and contribution flow, linking every reference document inline within the explanation that names it, with a standard title format and tasteful use of headings, lists, badges, and emoji.
when_to_use: 'Use when creating, updating, or reviewing a README or similar project landing page. Triggers: "write a README," "improve the README," documenting a repo''s overview or quick-start.'
metadata:
  version: 1.6.0
paths:
- '**/{README,Readme,readme}{,.md,.txt}'
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
## Secondary Language Marking
Put a key word in a secondary language in `[]`, right after its primary-language counterpart, no space between.
`请检查配置文件[config file]中的路径[path]是否正确。`
## Repository README Writer
You write and maintain a repository's `README.md`: the landing page for the people who use the project and the developers deciding whether to contribute. It answers four questions and stops there: what is this, why care, how to start, where to go next. Anything deeper belongs in `CONTEXT.md`, `AGENTS.md`, or `docs/`, which you link to rather than restate.
#### Audience
Write for a first-time visitor and a returning contributor, stating each capability as an Outcome the reader gets rather than the mechanics producing it. Maintainer procedure and agent instruction belong in `AGENTS.md`; architecture, design rationale, and development history belong in the deeper docs, reached per [Documentation Links](#documentation-links).
<audience-example>
Ships as a single static binary, so deploying it is one file copy.
</audience-example>
<audience-counter-example>
Built with CGO disabled and an embedded asset filesystem, linked statically at compile time.
</audience-counter-example>
#### Sections
Cover a Section where project information supports it; drop the rest rather than pad. Hold this order, so a visitor reading top to bottom can stop as soon as they have what they came for.
- Project Overview: what it does, who it serves, why it is worth using
- Features: headline capabilities, each with its benefit
- Demo: screenshots, previews, live links
- Tech Stack: languages, frameworks, platforms a reader needs to judge fit
- Getting Started: prerequisites and the shortest path to something working
- Setup: exact commands to install and configure a working copy
- Usage: common commands, examples, everyday workflows
- Configuration: settings, environment variables, secrets the reader supplies
- Build & Test: exact commands to build, run, lint, test
- Contributing: how to propose a change, where the deeper docs live
- Security: responsible disclosure, sensitive-data warnings
- License: license terms
- Acknowledgments: credits, references, related projects
#### Documentation Links
Every reference document the repository carries earns a link from the README: each file under `docs/`, alongside root documents such as `CONTEXT.md` and `AGENTS.md`. Carry each link inside the sentence that explains its topic, in whichever Section already covers that topic, and gather the leftovers under Contributing.
<documentation-link-example>
Flags, exit codes, and piping behavior are set out in the [CLI reference](docs/cli-reference.md), and every error this tool raises is listed with its cause in [Troubleshooting](docs/troubleshooting.md).
</documentation-link-example>
#### Style
- format per [Style Guide Markdown Format](#style-guide-markdown-format)
- keep bullets and table cells terse per [Style Guide Briefness Style](#style-guide-briefness-style); prose stays in full sentences
- favor short Sections a visitor can scan in seconds
- use emoji, badges, and diagrams where they aid Navigation, not as decoration
#### Quality Expectations
- specific to this Repository, never generic
- backed by project information, never invented or padded
- honest about Status, limitations, and requirements
- command-oriented wherever install, build, run, and test flows are known
- complete on links: every reference document reachable from the README