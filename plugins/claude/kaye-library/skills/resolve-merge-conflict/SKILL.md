---
name: resolve-merge-conflict
description: Resolves conflicts in a halted Git merge — reconciles both sides of every hunk into correct working-tree files, markers removed.
when_to_use: Triggers on a halted merge, rebase, cherry-pick, or pull; `<<<<<<<`/`=======`/`>>>>>>>` markers; or phrases like "resolve the conflicts," "fix the merge," "merge --continue is blocked." Not for branch strategy or merge commit messages.
metadata:
  version: 1.5.1
---

## Resolve Merge Conflict
You resolve a **halted Git merge**. Leave the working tree and index correct so the *user* can finish the merge.
#### Resolve
- fix **only** files Git reports as unmerged; read both sides with context first, and disambiguate with `git log`, `git diff`, `git show :1:/:2:/:3:path`
- reconcile **semantically**: imports, signatures, config keys, and call sites must still agree
- preserve intent from both branches; never take "ours" or "theirs" wholesale
- name the surviving path for delete/modify and rename conflicts
- regenerate lock and generated files, never hand-merge
- stop and ask when a resolution needs a decision you cannot infer
- remove every conflict marker; grep for residuals, confirm each file parses or compiles, run tests if cheap
- `git add` each path as soon as it is resolved
- touch only the working tree and index: no `merge --continue`, `commit`, `merge --abort`, or branch/tag/stash/worktree changes, since finishing or abandoning the merge is the user's call
#### Output
Per file: what each side changed, how you reconciled it, what to double-check. End by stating the index is staged and ready for `git merge --continue`.
### {[Claude:TodoWrite] Usage}
track resolution with the `TodoWrite` tool — one todo per unmerged path, marked complete only after its markers are gone and the file parses