---
name: coder-command-usage-message
description: writes command usage messages — the compact call-shape reference a command prints for `--help`, in errors, or atop a manual page
when_to_use: fires on "usage line", "usage message", "synopsis", `--help` text, argument syntax, or any command-line interface whose accepted call shapes need spelling out. Also fires when reviewing existing usage text for notation or ordering. Not for the prose option descriptions that follow it
metadata:
  version: 1.6.2
---

# Style Guide
## Letter Case
### Letter Case All Caps
uppercase words joined by underscores, eg: `TOTAL_PRICE`
## Command Usage Message
a usage message is the compact reference a command prints for `--help`, in an error, or atop its manual page. Its job is recognition at a glance: name the command, then show every accepted call shape with a small fixed notation, before any of it turns into prose
#### form
- name the command first, then its arguments and flags, in the order the parser expects them
- give one line per distinct call shape; do not cram every flag combination onto a single line — two spellings of a command get two usage lines, not one line straining to hold both
- put the required, common case first; variants and rare flags follow
#### notation
- write a required argument in [All Caps](#letter-case-all-caps), eg `COMMAND FILE LINE_PATTERN`
- wrap an optional argument or flag in square brackets, eg `[OPTIONAL_ARG]`, `[-r]`
- separate mutually exclusive choices with `|`, eg `[-c|-C]`
- pair a long flag with its short form as `--some-flag, -s`
- prefix a negating long flag with `no-`, eg `--no-some-flag, -S`
- use `*` to stand in for a family of related names, eg `command_print_in_* MESSAGE`
- keep an optional operand's brackets consistent wherever it reappears — in the call line and in its later description alike, eg `[LINE_PATTERN]` in both