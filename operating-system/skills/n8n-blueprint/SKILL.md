---
name: n8n-blueprint
description: Design an airtight n8n workflow blueprint before a builder creates nodes. Use for client automations, node-by-node specs, JSON contracts, error handling, test payloads, and single-LLM versus ensemble decisions.
---

# n8n Blueprint

Design the workflow; do not build nodes in the same pass unless the user explicitly asks after approving the blueprint.

## Required Output
```markdown
# Workflow: [name]
## Trigger
[Webhook, cron, Gmail Trigger, manual. Include exact schedule/path/event.]
## Node-by-Node Spec
Node 1 - [name] ([n8n node type])
- Purpose:
- Config:
- Input:
- Output:
- Failure path:
## Data Contracts
[Exact JSON request/response shape for every LLM, webhook, HTTP, sheet, or database step.]
## Error Handling
[Per node: failure mode, fallback, log target, alert owner, retry/stop rule.]
## Test Payloads
[Happy path plus edge cases, no-result path, malformed input, duplicate input.]
## Model Architecture
[Single LLM or multi-LLM ensemble. Include cost/accuracy tradeoff and final recommendation.]
## Build Handoff
[What the builder can implement now, what is blocked, what access/data is still needed.]
```

## JT-Specific Rules
- Query n8n MCP/node docs before specifying unfamiliar node fields.
- Prefer single LLM for deterministic extraction, routing, formatting, and simple classification.
- Use a 4-LLM cross-examination ensemble only when auditability or qualitative risk justifies the cost.
- Production n8n on Windows stays native Node + NSSM. Never recommend WSL2/Docker for that environment.
- Preserve `.n8n` and encryption keys before any migration.

## Quality Gate
The builder can implement without making design decisions.
