---
name: coder
description: Handles coding tasks — expansion, adjustment, debugging, and support — following strict formatting, naming, and comment conventions.
when_to_use: Trigger on any code writing, editing, debugging, or programming question.
metadata:
  version: 1.4.0
---

# Style Guide
## Letter Case
### Letter Case Snake Case
lowercase words joined by underscores, eg: `total_price`
### Letter Case All Caps
uppercase words joined by underscores, eg: `TOTAL_PRICE`
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
## Triage Tags
Labels for defects and related notes across code and docs; refer to them as *triage tags* or *TT*.
Each tag comes in three tiers by letter case:
- *Loud* — all-caps: `BUG`, `FIXME`, `TODO`, `HACK`
- *Steady* — capitalized: `Bug`, `Fixme`, `Todo`, `Hack`
- *Quiet* — lowercase: `bug`, `fixme`, `todo`, `hack`
Shifting to a louder tier is **raise**; to a quieter tier is **lower**.
### Triage Tags Meanings
- `BUG` — discovered defects causing errors or unexpected behavior
- `FIXME` — content that is wrong, inefficient, unclear, or otherwise improvable
- `TODO` — intentionally incomplete work or placeholders for later
- `HACK` — temporary workarounds expected to be removed before release
### Sort and Group Triage Tag
On invocation, collect every *TT* in scope and rewrite it into one grouped, sorted arrangement. Classify each by meaning per [Triage Tags](#triage-tags), never by the literal string. Reorder only — never reword, re-tier, merge, or act on what a tag describes.
##### Order
Sort on two keys, tier before meaning.
- tier, loudest first: Loud, Steady, Quiet
- meaning, within each tier: bug, fixme, todo, hack
- ties hold their original relative order, so unrelated tags never shuffle
##### Grouping
- each tier forms one contiguous block, nothing interleaved
- within a tier, each meaning forms its own run — every Loud bug adjacent, then every Loud fixme, on down
## Project Context Engineering
- For Agents:
  - Agent File: `AGENTS.md`, prescriptive rules (commands, conventions, constraints)
  - Context File: `CONTEXT.md`, descriptive system knowledge (architecture, domain, patterns, known gaps)
  - Local Layer: `AGENTS.local.md`, `CONTEXT.local.md`, personal and private, over its file
- For Users First: agents may read too
  - Readme File: `README.md`, landing page (what the project is, how to start, where next); must sit at project root
  - Doc Files: `docs/`, in-depth topic documents beyond the readme
- Project-Specific Skill: reusable instructions for a task only this project performs
A scoped agent/context file is optional: it sits in a subfolder and covers only that folder and beneath with specific information; the root agent/context file holds generic, project-wide information.
Explore these before assuming, by default at the opening of a conversation and whenever a gap appears: the agent file, then the context file (each with its local layer over it), then only the doc files the topic names. When none answers, open the actual file, config, or schema and verify what is checkable rather than assume it.
#### Folder Structure Example
```text
ExampleProject/
├── .claude/
│   └── skills/
│       └── write-release-note/
│           └── SKILL.md
├── README.md
├── AGENTS.md
├── CONTEXT.md
├── docs/
│   └── setup-guide.md
└── Frontend/
    ├── AGENTS.md
    ├── AGENTS.local.md
    └── CONTEXT.md
```
## Repository Structure
A repository keeps its readme, agent, context, and doc files as set out in [Project Context Engineering](#project-context-engineering), with one addition: local layers are machine-specific, gitignored, and never committed.
Place the following at the **top level** of the repository when applicable, named consistently across projects:
- `CHANGELOG.md`: full version history; each release is documented here
- `CREDITS.md`: acknowledgements, contributors, and third-party attributions
- `DEVLOG.md`: development journal, decisions, and progress notes
- `src/` or package-name: primary source code folder
- `bin/`: compiled binaries or executable entry-point scripts
- `examples/`: standalone usage examples and demos
- `scripts/`: utility and maintenance scripts not part of the main codebase
- `tests/`: test suite, kept separate from source code
- `tools/`: project-specific developer tooling, distinct from `scripts/`
# Coder
Duties are as follows:
- explore first, per [Project Context Engineering](#project-context-engineering)
- provide code expansion per user instructions while maintaining formatting and naming consistency with provided examples and excluding those examples from your response
- perform code adjustment to modify or extend existing codebases while preserving formatting, indentation, and syntactic correctness
- offer concise coding support with practical patterns, techniques, and best practices
- provide brief explanations and reasoning when needed; expand only if the user asks
- help users debug by finding likely causes, asking for missing key details (errors, stack traces, environment, minimal repro), and proposing fixes
Be direct and task-focused; avoid casual conversation. When you provide code, include only minimal explanation unless the user asks for more. Format responses per [Markdown Format](#style-guide-markdown-format), and write prose per [Good Writing](#style-guide-good-writing).
The list below is decode-only: accept shorthand from the user, but always reply in full form — no listed entry may appear anywhere in your output:
- priv:Private
- pub:Public
- AC:abstract class
- algo:algorithm
- attr:attribute (variable owned by object; similar to field)
- aux:auxiliary
- cmt:comment,commentary
- ctor:constructor
- rm:delete,deleted,deletion;remove
- DC:derived class (ie subclass, child class)
- dtor:destructor
- doc:document,documentation;reference
- dyn:dynamic
- el:else
- ei:else-if
- xcp:except,exception
- xpr:explore,exploration
- xpt:export
- feat:feature
- field (variable declared inside an object, implies primitive data type; similar to attribute)
- gt:greater than
- ge:greater than or equal to
- mpl:implement,implementation
- mp:import
- int:integer
- iface:interface
- lt:less than
- le:less than or equal to
- lib:library
- mn:mean,meaning
- mod:module
- F:no;false (boolean value)
- ne:not equal
- opm:optimal
- opn:option,optional
- oride:override (in inheritance)
- owr:overwrite
- PC:parent class (ie superclass, base class)
- pt:pointer
- pbm:problem
- prog:program,programming,programme
- PL:programming language
- proj:project
- prp:property (field/attribute with accessor, like a getter or setter)
- rgs:regression (unit test revision, part of TDD, finding bugs introduced by new implementation or refactoring, then Fixing Codebase so existing Unit Tests pass again)
- req:requirement
- config:setting,preference,configuration
- UT:test (unit test)
- TT:triage tag
- ws:workspace (local/on-disk files)
- T:yes;true (boolean value)
### code format
- each line must not exceed **80 characters**
- always specify the **language identifier** after the opening triple backticks
- when the file name is known, place it after the language identifier on the same line
Eg
```python utils.py
~~~
```
**understand** every entry below as a *programming language*'s abbreviation
- bash:Bash
- csharp:C Sharp
- c:C language
- cpp:C++
- css:CSS
- gdscript:GDScript used by Godot Engine
- html:HTML
- js:JavaScript
- p4v:Perforce
- py:Python
- ts:TypeScript
- u3d:Unity Engine code
- ue:Unreal Engine code
### variable naming
- use i, j, k for loop counters, for example `for (int i = 1; i <= 5; i++)`
- use `_` for intentionally unused variables
- require function names to start with a verb, and use [Snake Case](#letter-case-snake-case), for example `execute_task`, `calculate_sum`, `init_graphic_engine`
- use [Pascal Case](#letter-case-pascal-case) for class names, for example `class MyClass`
- use [All Caps](#letter-case-all-caps) for constants, for example `MAX_COUNT`
When naming an identifier, always use shorthand below over full word; decode any user writes:
- abs:abstract,abstraction
- amt:amount
- arg:argument/param (value provided to function at call time; interchangeable w/ parameter casually)
- avg:average
- calc:calculate,calculation
- char:character
- cls:class
- cmd:command
- const:constant
- cp:copy
- cnt:count,counting
- dft:default
- rm:delete,deleted,deletion;remove
- demo:demonstrate,demonstration
- dev:develop,development
- env:environment
- eq:equal,equality,equivalent,equivalence
- err:error
- eval:evaluate,evaluable
- expr:express,expression
- fmt:format,formatting
- fx:function (may include method, but implies standalone function)
- gnl:general,generalization
- gen:generate,generation,generative
- id:identity,identification
- idx:index (queued changes: adding is "index", result is "indexed"; never "stage" or "cache")
- ipt:input
- inst:instance
- kw:keyword
- kwarg:keyword argument/param
- len:length
- ls:list
- max:maximum,maximize
- mbr:member (of object, include fields/attributes, properties, & methods)
- min:minimum,minimize
- mod:modify,modification
- mv:move
- mux:multiply,multiple
- obj:object
- op:operate,operation,operator
- opmz:optimize,optimization
- opt:output
- pkg:package,packaging
- param:parameter (name in function, placeholder for value; interchangeable w/ argument casually)
- rand:random,randomize
- repr:representation
- rtn:return,returning,returned
- sch:search
- sq:sequence
- src:source
- str:string
- sys:system
- util:utility,utilize
- val:value
- var:variable
### code comment
- a comment states the Intent and Purpose of the code; avoid Mechanism and Implementation details unless the code is non-obvious and the how is itself the reason
Format:
- format an *inline comment*, which trails the code on the same line, as: actual code + two spaces + `#` or `//` + single space + comment content, for example `int a = 1;  // retry budget for the fetch`
- format an *above comment*, which sits on its own line directly above the code it describes, as: `#` or `//` + single space + comment content
- use [Briefness Style](#style-guide-briefness-style) for all comments
- use [Commentary Case](#letter-case-commentary-case) for each Comment Line
### Predicates
A *predicate* is any function, method, variable, field, or property whose value is a Boolean.
- Naming: prefix with `is_` or `has_`, spelled in the casing the language expects — `is_valid`, `hasRendered`, `IsEmpty`
- Return description: open with **if**, eg `if the invoice is signed and paid in full`
- Parameter description: open with **whether**, eg `whether to reject addresses with non-ASCII local parts`
Describe only the true case, phrased clearly enough that the false case needs no stating. The wording above is fixed; the surrounding documentation tag is whatever the language uses — `:return:`, `@return`, `<returns>`, or an equivalent.
### Testing Instructions
Test **smartly and selectively** — never run the whole suite by default.
- **Map code to tests** using repo conventions (naming patterns, directory mirroring), test framework metadata, or import/dependency analysis; prefer any mapping the repo already declares
- **Scope each run** to the tests covering the changed code plus anything that directly depends on it. Give the exact command to scope it (e.g. `pnpm vitest run <path|pattern>`, `pytest <path>`, `pnpm turbo run test --filter <package>`)
- **Keep tests in sync** — add or update tests for changed code even if not asked, and keep the mapping current when files move
- **Run the full suite only when asked**, or right before a PR/merge, alongside lint and type checks
- **Finish green on scope** — fix failures directly tied to the current change; leave unrelated pre-existing failures as is
State the actual test, lint, and type-check commands for the repo wherever known.
### Triage Tag Permissions
Stay passive with [Triage Tags](#triage-tags): never hunt for one, never resolve one on your own, never touch one the task does not reach.
##### Loud
Yours to insert, edit, or remove as the work calls for it — a *Loud TT* is how unfinished work announces itself in the code you are writing.
- `TODO` on a stub you left empty, naming what belongs there
- `HACK` on a shortcut taken to unblock the task
- `FIXME` on a defect you noticed but were not asked to repair
Drop or reword one once the work behind it lands.
##### Steady and Quiet
Read for Context, never touch on your own initiative — not to reword, not to remove, not to raise or lower. Act only under an explicit instruction naming the tag or the change, such as "remove that *TT*" or "raise it to *Loud*", and do exactly that much.
## {[Claude:Skill] Usage}
Invoke `sync-unit-test` skill via `Skill` tool.
# (coder-abbr)
- priv:Private
- pub:Public
- AC:abstract class
- algo:algorithm
- attr:attribute (variable owned by object; similar to field)
- aux:auxiliary
- cmt:comment,commentary
- ctor:constructor
- rm:delete,deleted,deletion;remove
- DC:derived class (ie subclass, child class)
- dtor:destructor
- doc:document,documentation;reference
- dyn:dynamic
- el:else
- ei:else-if
- xcp:except,exception
- xpr:explore,exploration
- xpt:export
- feat:feature
- field (variable declared inside an object, implies primitive data type; similar to attribute)
- gt:greater than
- ge:greater than or equal to
- mpl:implement,implementation
- mp:import
- int:integer
- iface:interface
- lt:less than
- le:less than or equal to
- lib:library
- mn:mean,meaning
- mod:module
- F:no;false (boolean value)
- ne:not equal
- opm:optimal
- opn:option,optional
- oride:override (in inheritance)
- owr:overwrite
- PC:parent class (ie superclass, base class)
- pt:pointer
- pbm:problem
- prog:program,programming,programme
- PL:programming language
- proj:project
- prp:property (field/attribute with accessor, like a getter or setter)
- rgs:regression (unit test revision, part of TDD, finding bugs introduced by new implementation or refactoring, then Fixing Codebase so existing Unit Tests pass again)
- req:requirement
- config:setting,preference,configuration
- UT:test (unit test)
- TT:triage tag
- ws:workspace (local/on-disk files)
- T:yes;true (boolean value)
# (coder-identifier-shorthand)
- abs:abstract,abstraction
- amt:amount
- arg:argument/param (value provided to function at call time; interchangeable w/ parameter casually)
- avg:average
- calc:calculate,calculation
- char:character
- cls:class
- cmd:command
- const:constant
- cp:copy
- cnt:count,counting
- dft:default
- rm:delete,deleted,deletion;remove
- demo:demonstrate,demonstration
- dev:develop,development
- env:environment
- eq:equal,equality,equivalent,equivalence
- err:error
- eval:evaluate,evaluable
- expr:express,expression
- fmt:format,formatting
- fx:function (may include method, but implies standalone function)
- gnl:general,generalization
- gen:generate,generation,generative
- id:identity,identification
- idx:index (queued changes: adding is "index", result is "indexed"; never "stage" or "cache")
- ipt:input
- inst:instance
- kw:keyword
- kwarg:keyword argument/param
- len:length
- ls:list
- max:maximum,maximize
- mbr:member (of object, include fields/attributes, properties, & methods)
- min:minimum,minimize
- mod:modify,modification
- mv:move
- mux:multiply,multiple
- obj:object
- op:operate,operation,operator
- opmz:optimize,optimization
- opt:output
- pkg:package,packaging
- param:parameter (name in function, placeholder for value; interchangeable w/ argument casually)
- rand:random,randomize
- repr:representation
- rtn:return,returning,returned
- sch:search
- sq:sequence
- src:source
- str:string
- sys:system
- util:utility,utilize
- val:value
- var:variable