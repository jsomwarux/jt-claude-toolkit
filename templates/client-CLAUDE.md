# CLAUDE.md — Client Engagement (template)

> Keep this file thin and project-specific. Reusable methodology (proposals, blueprints,
> playbooks, research) lives in the `consulting-toolkit` plugin, not here. This file holds
> only what is true for THIS client: infrastructure, paths, credentials references, and
> standing constraints. The Altmark values below are a worked example — replace per client.

## Client
- Company: <Family-owned NYC real estate operator, 3M+ sq ft> (anonymize in any external doc)
- Primary contact: <Name, role, email, phone>
- IT contact: <Name, availability>
- Engagement: <N workflows, $total implementation + $monthly support>

## What we're building
1. Insurance / COI expiration tracking — <status>
2. Loan management — <status>
3. WhatsApp AI knowledge bot (RAG) — <status>
4. Bank deposit report → QuickBooks reconciliation — <status>
5. Cash management / overdraft prevention — <status>
6. Rent delinquency outreach — <status>

## Infrastructure (Beelink, native Windows)
- n8n runs as a native Windows service via NSSM (WSL2/Docker failed in production — never use them here).
- URL: `http://100.94.117.7:5678`  ·  SSH: `ssh JT@100.94.117.7`
- Data: `C:\n8n\.n8n` (preserve this dir + the encryption key on any migration)
- App: `C:\n8n\app`  ·  Startup: `C:\n8n\start-n8n.cmd`  ·  NSSM: `C:\n8n\nssm.exe`
- Service: `C:\n8n\nssm.exe status|start|stop|restart n8n`  ·  Logs: `C:\n8n\logs\`
- Sleep/hibernate disabled via powercfg. Google OAuth published (permanent tokens).

## Hard constraints (learned the hard way)
- Never run WSL2/Docker for production n8n on Windows. Native Node + NSSM only.
- Read File nodes on the NSSM service are restricted to `C:\WINDOWS\system32\config\systemprofile\.n8n-files`.
- Gmail Trigger node may show "Install this node" due to a version mismatch with n8n 2.18.4 — recreate the node manually.

## Credential & resource references (values in knowledge.md, never commit secrets)
- Rent Delinquency Google Sheet ID: `1YoE91mQSxP2yGaYPIWZtDILhULjPXIXIGyxxazKvqoo`
  - Tabs: Outreach Log, Report Processing Log, Do Not Contact
- APIs in use: Claude API, AppFolio, Plaid, Twilio, Conductor (QuickBooks Desktop), Google Workspace.

## Open items
- Still needed from client: email templates, sender address, AppFolio subject line, reply-to address.
