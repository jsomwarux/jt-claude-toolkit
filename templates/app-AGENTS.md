# AGENTS.md — App / Product (template)

> Use AGENTS.md (not CLAUDE.md) for any repo where both Codex and Claude Code work the
> codebase — both tools read this file, giving one source of truth. (Symlink
> `CLAUDE.md -> AGENTS.md` if you also want the CLAUDE.md name.) Keep it thin and
> project-specific; the 8-phase build process lives in the `product-builder` plugin.
> The Action Arena values below are a worked example — replace per app.

## Project
- Name: <Action Arena>
- What it is: <free-to-play iOS sports prediction app; fantasy-league structure applied to
  game predictions with virtual coins; three pick types: straight, parlay, teaser>
- Stage: <active development / testing>

## Stack
- React Native + Expo (mobile), Supabase (backend/auth/db).
- Tooling split: Codex for functional work, Claude Code for UI polish. Both read this file.

## Architecture
- <Key directories, navigation structure, state management>
- <Supabase schema: tables and the picks/coins/league data model>
- <Where the three pick types are validated and scored>

## Constraints & conventions
- App Store compliance: NO gambling vocabulary anywhere (no "bet", "wager", "odds", "stake").
  Use prediction/pick/coins language. Re-check this on every user-facing string.
- <Coding conventions: TypeScript strict, functional components, etc.>
- <Test plan location and how to run it>

## Build & run
```bash
# fill in real commands
npx expo start
npm run typecheck
npm run lint
npm test
```

## Quality gates (before merge)
- Compliance string scan passes (no gambling terms).
- Type check + lint + tests pass with real execution.
- Run the `quality-pass` agent on the diff (LARP + slop check).

## Tasks
- `tasks/todo.md`, `tasks/lessons.md` — carry context and lessons across sessions.
