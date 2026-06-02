---
name: build-playbook
description: Write a step-by-step build playbook so simple a non-technical person could follow it. Use this skill whenever the user asks for a playbook, a step-by-step guide, a runbook, build instructions, an implementation guide, or "exact steps" for setting up an n8n workflow, an automation, an integration, or any multi-step technical build. Always use this when the user wants the exact order of actions plus the exact prompts to hand to their n8n builder agent. Produces a single self-contained document in JT's established playbook format.
---

# Build Playbook

Produce a build playbook in JT's house format: dead-simple, sequential, and complete enough that someone with zero context could execute it without asking a single question. The reader is often JT mid-build or a junior helper, so assume nothing and leave no decision implicit.

## Output format

ALWAYS follow this structure:

```
# USE CASE: <Name> — $<Price>
## <Phase label if staged>

## What This Workflow Does
<2–4 plain-English sentences. No jargon. Describe the outcome, not the tech.>

## Before You Start (Prerequisites)
<Bullet list of every credential, ID, file, and access needed up front, with where to get each.>

## Step 1: <Action>
<Exact thing to do. If it's a prompt for the n8n builder agent, put it in a fenced block labeled "Prompt for n8n agent:".>

## Step 2: <Action>
...

## Test It
<Exact test input, expected output, and how to know it worked.>

## Go Live
<What to flip on, what to monitor the first day.>
```

## Writing rules

- One action per step. If a step has an "and," it's probably two steps.
- Every prompt the user must paste into their n8n builder agent goes in its own fenced code block, written out in full — never "tell the agent to build the webhook," always the literal prompt.
- Spell out where to click and what to type. "Open the Twilio Console → Messaging → WhatsApp → Senders" beats "configure Twilio."
- Surface known pitfalls inline at the step where they bite, not in a separate appendix. Examples from past builds: Gmail Trigger node version mismatch on Beelink n8n 2.18.4 (recreate the node manually if "Install this node" appears); n8n Read File nodes on an NSSM Windows service are restricted to `C:\WINDOWS\system32\config\systemprofile\.n8n-files`; never run WSL2/Docker for production n8n on Windows.
- Always end with a concrete test using sample/test data before real client data, and a delivery step where the client verifies accuracy.
- Name the exact Google Sheet IDs, tab names, file paths, and node types when known. Vague references force the reader to guess.

## Length

These run long by design — completeness beats brevity. Save as a standalone Markdown file (or PDF if asked) rather than answering inline, since the user executes from it over time.
