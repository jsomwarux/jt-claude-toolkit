# JT Claude Toolkit

A Claude Code plugin marketplace that extracts JT's repeated work into reusable, portable
extensions — so per-project `CLAUDE.md`/`AGENTS.md` files stay thin and the methodology
lives in one installable place instead of being re-tuned in every repo.

## The organizing rule

- **Skills** = repeatable procedures and output formats. Model-invoked ones auto-load when
  relevant; the workflow ones are user-invocable only (`disable-model-invocation: true`) so
  they behave like classic slash commands.
- **Agents** = delegated roles with their own context (strategist, builder, quality pass).
- **Plugins** = the bundle of the above, installed once and reused across projects.
- **CLAUDE.md / AGENTS.md** = thin, per-project context only (see `templates/`).

## Plugins

### consulting-toolkit
Client delivery. Auto-invoked skills: `opportunity-research`, `n8n-blueprint`,
`build-playbook`, `proposal-pdf`, `resume-tailor`. User-invoked skills:
`new-client`, `build-workflow`. Agents: `workflow-strategist`, `n8n-builder`.

### product-builder
App/product builds. Auto-invoked skill: `build-phases` (8-phase workflow). User-invoked
skill: `ship`. Agent: `quality-pass` (simplify -> de-slop -> LARP assessment -> real
verification). Formatting is explicit/project-native; no global format-on-save hook is enabled
by default.

### operating-system
JT-specific operating-system workflows mirrored from OpenClaw's source of truth. Skills:
`ai-context-os`, `client-proof-capture`, `linkedin-corpus`, `n8n-blueprint`, `proposal-pdf`,
and `product-build-loop`. Agents: `workflow-strategist`, `product-quality-pass`.

## Install

```bash
# from a local clone (fastest for iteration)
/plugin marketplace add ./jt-claude-toolkit
/plugin install consulting-toolkit@jt-toolkit
/plugin install product-builder@jt-toolkit
/plugin install operating-system@jt-toolkit
```

Once pushed to GitHub, other machines add it by repo (relative source paths only resolve
when added via git, so use the GitHub form for distribution):

```bash
/plugin marketplace add jsomwarux/jt-claude-toolkit
```

Plugin skills are always namespaced. Invoke the user-facing workflows as:
`/consulting-toolkit:new-client <company>`, `/consulting-toolkit:build-workflow <client> <workflow>`,
`/product-builder:ship <message>`. After edits, run `/reload-plugins` to pick them up.

## Templates (not a plugin)

`templates/` holds thin per-project config to copy into each repo:
- `client-CLAUDE.md` — per-client infra, paths, constraints with sanitized placeholders.
- `app-AGENTS.md` — per-app stack + gates (Action Arena worked example; AGENTS.md so Codex
  and Claude Code share one source of truth).
- `ensemble-CLAUDE.md` — the 4-LLM ensemble repo engine guide.

## Validate before publishing

```bash
claude plugin validate .
```

Tighten a skill's `description` if it under- or over-triggers, and move anything you find
yourself re-explaining in a project's CLAUDE.md up into a skill here.
