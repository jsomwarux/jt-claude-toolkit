# product-builder

Product/app build loop for Claude Code.

**Skill (auto):** build-phases — 8-phase workflow (plan -> implement -> keep going -> quality
-> test -> LARP -> de-slop -> prod).
**Skill (user-invoked):** ship — quality pass, then commit/push/PR (`/product-builder:ship`).
**Agent:** quality-pass — simplify -> de-slop -> LARP assessment -> real verification.
**Hook:** PostToolUse format-on-save — runs `prettier --write` on edited files if available,
fail-safe (no-op in repos without prettier). Remove `hooks/hooks.json` to disable.

Use AGENTS.md (see ../templates/app-AGENTS.md) in repos shared by Codex + Claude Code.
