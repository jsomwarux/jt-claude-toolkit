---
name: new-client
description: Scaffold a new client engagement and run opportunity research. Invoke explicitly as /consulting-toolkit:new-client followed by a company name or website.
disable-model-invocation: true
---

# New Client

Set up a new client engagement. The client is: $ARGUMENTS

Do the following in order:

1. Create the client folder structure:
   - `clients/<slug>/README.md` — company info, contact, what we're building, total engagement size.
   - `clients/<slug>/brief.md` — use cases, order of operations, known pitfalls.
   - `clients/<slug>/knowledge.md` — credential references, API endpoints, Google Sheet IDs, file paths (placeholders until provided; never commit secrets).
2. Use the `opportunity-research` skill to research the company/vertical and produce a ranked shortlist of automation opportunities, then save it into `brief.md`.
3. List what you still need from the client (templates, sender addresses, IDs, access) as an explicit checklist.

If the company name is all you were given, research from the web first, then ask once for anything you can't infer (contact, systems in use, primary pain point).
