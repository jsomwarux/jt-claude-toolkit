---
name: n8n-blueprint
description: Design a copy-paste-ready n8n workflow blueprint for a builder agent. Use this skill whenever the user wants to design, architect, or spec an n8n workflow or automation — including node-by-node specs, JSON schemas, error handling, and test payloads — for a client automation. Always use this when the output is an airtight build spec meant to be handed to an n8n builder agent via MCP, as opposed to a client-facing playbook. Also use when deciding whether a workflow step should use a single LLM or a multi-LLM ensemble.
---

# n8n Workflow Blueprint

Act as the Workflow Strategist: produce an airtight, node-by-node blueprint that a separate n8n builder agent can implement with no further design decisions. You design; you do not build. Every ambiguity you leave becomes a bug the builder ships.

## Required output sections

ALWAYS produce, in this order:

```
# Workflow: <Name>
## Trigger
<What fires it: webhook, cron, Gmail Trigger, manual. Exact schedule/path.>

## Node-by-Node Spec
Node 1 — <Name> (<n8n node type>)
  Purpose: ...
  Config: <exact fields>
  Input: <shape>
  Output: <shape>
Node 2 — ...

## Data Contracts
<For every LLM call or HTTP step, the exact JSON the node sends and the exact JSON it must return. Use real field names.>

## Error Handling
<Per node: what can fail, the fallback path, what gets logged where, who gets alerted.>

## Test Payloads
<Concrete sample inputs the builder can paste to verify each branch, including edge cases and the "no result found" path.>

## Ensemble vs Single-LLM Recommendation
<Explicit call with justification — see below.>
```

## LLM call conventions

- Anthropic HTTP Request node: `POST https://api.anthropic.com/v1/messages`. Verify the current model ID at docs.claude.com before writing a new workflow; keep deployed workflows on their tested model string unless you re-test. Always specify `max_tokens` and parse `content[0].text`.
- When a node must return structured data, instruct the model to return ONLY JSON, no markdown or preamble, and have the next node parse it. Include the exact JSON schema in the prompt.
- For routing steps, output a small JSON object (e.g. `{"data_source": "...", "search_query": "...", "clarification_needed": false}`) and branch with a Switch node.

## Ensemble vs single-LLM decision

Make an explicit recommendation every time, then flag it for the user's final cost/accuracy call. Heuristics:

- **Single LLM** for deterministic extraction, routing, and formatting where one capable model is reliable. Cheaper and simpler.
- **4-LLM ensemble with cross-examination** when the task is high-stakes qualitative synthesis, needs an audit trail/defensibility, or benefits from catching model-specific bias (e.g. insurance claims triage, risk scoring). Stage 1: identical prompt to all models in parallel. Stage 2: each model sees the others' outputs and challenges them. Then synthesize. Note the added cost (roughly 2x the model calls) so the user can weigh it.

## Hard-won n8n constraints to bake in

- Production n8n on Windows runs as a native Node service via NSSM — never WSL2/Docker.
- Read File nodes on an NSSM service are restricted to `C:\WINDOWS\system32\config\systemprofile\.n8n-files`.
- Gmail Trigger node versions can mismatch between the agent build and the target n8n (e.g. 2.18.4) — flag that the node may need manual recreation.
- Preserve the `.n8n` directory and encryption key across any migration.
