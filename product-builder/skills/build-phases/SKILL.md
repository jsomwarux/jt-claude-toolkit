---
name: build-phases
description: Drive an app or product build through a disciplined 8-phase workflow. Use this skill whenever the user is building a feature, an app, or a tool from scratch and wants a structured build process rather than ad-hoc coding — especially for React Native/Expo apps, Next.js dashboards, or macOS tools. Always use this when the user says "build", "implement this properly", "ship a real version", or wants to avoid AI slop and half-finished implementations.
---

# Build Phases

Drive non-trivial builds through eight phases. The point is to reach genuinely production-ready code instead of a plausible-looking draft. Don't skip the assessment phases — they are where slop and fake implementations get caught.

## The phases

1. **Plan & Research.** Clarify the goal, identify constraints, research patterns (use Context7 MCP for current library docs to avoid hallucinated APIs), outline architecture, list risks. Produce a written plan and get agreement before implementing.
2. **Implement.** Follow the plan sequentially. Write complete code, handle edge cases, commit in logical chunks.
3. **Keep going.** Continue through all tasks to completion without stopping between items. Summarize at the end.
4. **Quality pass.** Remove dead code, redundancy, and over-abstraction; simplify verbose logic; enforce consistent style.
5. **Testing.** Go beyond the happy path: boundaries, error handling, integration points, async behavior. No mocks of the code under test.
6. **LARP assessment.** Critically evaluate whether the code is real or performative. Fix every stub, fake, or swallowed error.
7. **Slop cleanup.** Remove AI-generated cruft. Keep value, delete noise.
8. **Production validation.** All tests pass with real execution; error handling with proper logging; config externalized; dependencies pinned and scanned.

Phases 4–8 map to the `quality-pass` subagent — delegate to it when you want a fresh skeptical context.

## Stack conventions

- Mobile: React Native + Expo + Supabase. Web: Next.js. macOS: native menu-bar app.
- When a project uses both Codex (functional work) and Claude Code (UI polish), keep shared context in `AGENTS.md` so both tools honor one source of truth.
- Use a `tasks/` directory (`tasks/todo.md`, `tasks/lessons.md`) to track work and capture lessons across sessions. Initialize with `mkdir tasks && touch tasks/todo.md tasks/lessons.md`.

## Communication protocol

Before significant work, state the recommended approach and what the workflow will look like, then proceed once agreed. Use plan mode for anything that ends in a PR. Keep CLAUDE.md/AGENTS.md high-signal and project-specific — push reusable methodology out into skills and plugins instead of bloating per-project config.
