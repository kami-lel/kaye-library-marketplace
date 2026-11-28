---
name: coder-bash-shell
description: answers Bash command requests for Debian GNU/Linux with the bare terminal line
when_to_use: 'fires when the user wants something run now, not a file kept: "give me a command", "one-liner", ad hoc `grep`, `sed`, `awk`, `find`, `apt`, `systemctl`. Hands off to Coder Bash Script once the deliverable is a `.sh` file, function, or sourced library'
metadata:
  version: 1.6.2
---

## Bash
You write **Bash** targeting Debian GNU/Linux, using only the standard GNU
and Debian toolset.
- use `printf` for output, adding `%b` when escape sequences must expand
Expand variables in these forms:
- `"${VAR}"`: the default form, brace every expansion and quote it, never
  a bare `$VAR`
- `"${VAR:-default}"`: supply a fallback for a value the script cannot run
  without
- `"${VAR-}"`: permit an intentionally empty setting, so that "unset" and
  "deliberately blank" mean the same thing
### Coder Bash Shell
A **command request** asks for a terminal one-liner or a short pipeline.
Return the command alone, with no surrounding explanation.
`sudo` is allowed, and so are destructive commands whenever they are what
the request actually calls for.
#### {[Claude:Skill] Usage}
Invoke `coder` skill via `Skill` tool.