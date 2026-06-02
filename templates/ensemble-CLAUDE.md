# CLAUDE.md — Ensemble Blueprint Repo (template)

> This repo is the reusable 4-LLM ensemble ranking architecture. New verticals are spun up
> by adding a niche config, not by rewriting the engine. Keep niche specifics in
> `niches/<name>/niche-config.md`; keep this file about the shared engine. Fill the
> EXACT code details (endpoints, dict shapes, payloads) from the actual codebase — have
> Eve write the precise version if you're unsure.

## Architecture (the flow)
Frontend trigger → Python engine → 4 parallel LLM calls (Stage 1, identical prompt) →
cross-examination (Stage 2, each model sees the others) → synthesis → callback → database.

- Models: Claude, GPT, Gemini, Grok. Same prompt to all in Stage 1.
- Stage 2 is the moat: each model challenges the others' reasoning on the same evidence.
- Prefer a shared deterministic Evidence Pack feeding all models (so they argue over
  interpretations of the same facts, not different facts). Use hard vetoes over weighted
  averages in adversarial domains. Don't let final synthesis be a single model.

## Key code references (fill from codebase)
- `main.py`: `AnalyzeRequest` fields — <list exact fields>
- `config.py`: `MODELS` dict shape — <exact format for defining the 4-model ensemble>
- Endpoints, ports, HTTP methods — <exact>
- Callback payload shape (engine → frontend) — <exact fields>
- Prompt file format and placeholder syntax — <how variables are injected into .txt prompts>

## Adding a new niche
1. Create `niches/<name>/niche-config.md` with: scoring dimensions table, score modifiers,
   UI decisions, infrastructure notes, model behavior notes.
2. Rename the request fields per niche; reuse the engine.
3. Existing niches as references: crypto (Nash-Satoshi Oracle), skincare (Glow Index).

## Notes
- Glow Index lives at glowindex.co (GoDaddy domain → Replit deployment).
- The ensemble framing is marketing copy, not a technical moat — real differentiation is in
  data inputs, use-case fit, and distribution. Down-rank verticals where the ensemble is just
  dressing up a deterministic calculation.
