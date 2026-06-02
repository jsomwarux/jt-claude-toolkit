# CLAUDE.md — Client Engagement (template)

> Keep this file thin and project-specific. Reusable methodology (proposals, blueprints,
> playbooks, research) lives in the `consulting-toolkit` plugin, not here. This file holds
> only what is true for THIS client: infrastructure, paths, credentials references, and
> standing constraints. Do not include live IPs, private Sheet IDs, credentials, client secrets,
> or real client-only workflow details in a public repo template.

## Client
- Company: <Client profile / anonymized public description>
- Primary contact: <Name, role, email, phone>
- IT contact: <Name, availability>
- Engagement: <N workflows, $total implementation + $monthly support>

## What we're building
1. <Workflow / deliverable> — <status>
2. <Workflow / deliverable> — <status>
3. <Workflow / deliverable> — <status>

## Infrastructure
- Runtime: <n8n native Windows service / hosted n8n / other>
- URL: `<private URL or placeholder>` · SSH/access: `<credential reference only>`
- Data path: `<path>` (preserve workflow data and encryption keys on any migration)
- App path/log path/service command: `<paths or commands>`
- Auth/OAuth status: `<credential reference only; never paste token values>`

## Hard constraints (learned the hard way)
- Never run WSL2/Docker for production n8n on Windows. Native Node + NSSM only.
- Read File nodes on the NSSM service are restricted to `C:\WINDOWS\system32\config\systemprofile\.n8n-files`.
- Gmail Trigger node may show "Install this node" due to a version mismatch with n8n 2.18.4 — recreate the node manually.

## Credential & resource references (values in knowledge.md, never commit secrets)
- Google Sheet / Airtable / CRM IDs: `<store exact IDs in private knowledge.md, not public templates>`
- APIs in use: `<API names only; credentials live in approved secret stores>`

## Open items
- Still needed from client: email templates, sender address, AppFolio subject line, reply-to address.
