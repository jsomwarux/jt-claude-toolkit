---
name: product-build-loop
description: "Run JT's product/app build loop for real features, apps, dashboards, and tools: plan, implement, test, quality pass, LARP assessment, production validation, and shipping discipline."
---

# Product Build Loop

Use for non-trivial product work in apps, dashboards, websites, and internal tools.

## Workflow
1. Read project `CLAUDE.md`, `AGENTS.md`, and any `tasks/lessons.md`.
2. Create or update `tasks/todo.md` unless the change is a one-liner.
3. Plan the smallest useful shipped version.
4. Implement in logical chunks.
5. Run the quality pass: simplify, de-slop, check for stubs/fake data/swallowed errors/mocks of the code under test.
6. Verify with real commands: build, typecheck, lint, tests, and UI/browser checks when relevant.
7. Route proof/portfolio/content only when the build is substantive and verified.

## Output
Return what changed, what got simplified, what fake-implementation risk was checked, exact verification commands/results, and remaining risks.
