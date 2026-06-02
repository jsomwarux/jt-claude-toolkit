---
name: ship
description: Run a final quality pass, then commit, push, and open a PR. Invoke explicitly as /product-builder:ship followed by a commit message or PR title.
disable-model-invocation: true
---

# Ship

Ship the current work. Commit message / PR title: $ARGUMENTS

Do the following in order:

1. Delegate to the `quality-pass` agent: simplify, de-slop, run a LARP assessment, and verify with real build/test/lint execution. Do not proceed if verification fails — report what's broken instead.
2. Once clean: `git status`, then `git add -A`, then `git commit -m "$ARGUMENTS"`.
3. Push to the current branch.
4. Open a PR with a description summarizing the change, the test results, and anything reviewers should scrutinize.

Never use `--dangerously-skip-permissions`. If a needed command isn't pre-allowed, ask rather than forcing it.
