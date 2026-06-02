---
name: ship
description: Run a final quality pass and prepare a safe ship handoff. Invoke explicitly as /product-builder:ship followed by a commit message or PR title.
disable-model-invocation: true
---

# Ship

Ship the current work. Commit message / PR title: $ARGUMENTS

Do the following in order:

1. Delegate to the `quality-pass` agent: simplify, de-slop, run a LARP assessment, and verify with real build/test/lint execution. Do not proceed if verification fails — report what's broken instead.
2. Run `git status` and inspect the diff. Do not stage unrelated changes.
3. Stage only the files that belong to this work.
4. Commit with `$ARGUMENTS` only after verification passes and the staged diff is scoped.
5. Push/open a PR only when the user or repo workflow expects it. Otherwise report the exact verification results and the commit/PR-ready state.

Never use `--dangerously-skip-permissions`. Never use `git add -A` in a dirty worktree unless the diff was inspected and all changes belong to the task.
