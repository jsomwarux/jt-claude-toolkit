---
name: build-workflow
description: Design and prepare an n8n workflow for a client, from blueprint to build-ready playbook. Invoke explicitly as /consulting-toolkit:build-workflow followed by a client slug and workflow name.
disable-model-invocation: true
---

# Build Workflow

Prepare a workflow for build. Input: $ARGUMENTS (expected: client slug + workflow name, e.g. "altmark rent-delinquency-outreach").

Do the following in order:

1. Read `clients/<slug>/brief.md` and `clients/<slug>/knowledge.md` for context.
2. Delegate to the `workflow-strategist` agent (or use the `n8n-blueprint` skill) to produce the full node-by-node blueprint, data contracts, error handling, test payloads, and the ensemble-vs-single-LLM recommendation.
3. Use the `build-playbook` skill to convert the approved blueprint into a child-simple, step-by-step playbook with the exact prompts to hand to the n8n builder agent.
4. List anything still required from the client before the build can start.

Do not start building nodes until the blueprint is reviewed. Stop and present the blueprint and playbook first.
