---
name: working-with-git
description: Sets the Git working terms and the actions that need explicit approval, so edits stay in the workspace beside the user.
when_to_use: 'Trigger on any work in a Git repository: editing files, indexing, committing, branching, stashing, or running `git` commands. Not for writing the commit message itself (use `commit-sense`).'
metadata:
  version: 1.6.2
---

## Working with Git
Use these Git terms, no synonyms. Abbreviations are decode-only: never write them in a reply.
- branch
- gi:commit only the indexed (including unknown changes; workspace untouched)
- g:perform git commit (only changes made in this conversation, leave others untouched; ask if unsure)
- idx:index (queued changes: adding is "index", result is "indexed"; never "stage" or "cache")
- ig:index all workspace changes, commit (including unknown ones)
- stash
- ws:workspace (local/on-disk files)
- wt:worktree (main worktree unless a linked one is named)
----
- edit in the workspace; index your own changes when done or partly done
- run `git status` or `git diff` only when the codebase differs from what you expect
#### Working Alongside the User
- the user may work in the same workspace or worktree at the same time. Treat any change you did not make as theirs: never revert, index, or commit it
- if a change you did not make blocks your work, stop and report
#### Actions Needing Explicit Approval
Run only when the user names the exact action in the same turn:
- Rewrite History: `git commit --amend`, `git rebase`, `git reset`, `git cherry-pick`
- Discard Work: `git reset --hard`, `git checkout .`, `git restore .`, `git clean -f`, `git stash drop`, `git branch -D`
- Publish: `git push`, `git push --force`, `git tag`, `gh pr create`
- Sweep or Bypass: `git add -A`, `git add .`, any command with `--no-verify`
### {[Claude:Skill] Usage}
To commit, invoke the `commit-sense` skill via the `Skill` tool.
Never devise your own commit message format, nor run `git commit` outside it.