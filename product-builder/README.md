# product-builder

Product/app build loop for Claude Code.

**Skill (auto):** build-phases — 8-phase workflow (plan -> implement -> keep going -> quality
-> test -> LARP -> de-slop -> prod).
**Skill (user-invoked):** ship — quality pass, then commit/push/PR (`/product-builder:ship`).
**Agent:** quality-pass — simplify -> de-slop -> LARP assessment -> real verification.

No global format-on-save hook is enabled by default. Run project-native formatting commands
explicitly so mixed repos do not pick up unrelated diffs.

Use AGENTS.md (see ../templates/app-AGENTS.md) in repos shared by Codex + Claude Code.
