---
name: resume-tailor
description: Tailor JT's resume to a specific role or company as a polished two-page Word document. Use this skill whenever the user wants a resume built, updated, tailored, or optimized for a particular job, role, or company. Always use this when producing a resume .docx — it enforces the anonymized-client framing, independent-consultant positioning, fixed metrics, and formatting rules so the output is correct on the first pass. For the underlying Word mechanics, also read the docx skill.
---

# Resume Tailor

Produce a tailored, two-page Word resume for JT that maps his real work to the target role. Always pair this with the `docx` skill for the actual document mechanics (`/mnt/skills/public/docx/SKILL.md`).

## Positioning rules (non-negotiable)

- **Independent consultant framing.** JT is an independent AI implementation consultant, not an employee of any product. No "Opticfy" branding or company-of-one naming anywhere.
- **Anonymize client names.** Never name clients. Describe them by profile: e.g. "a family-owned NYC real estate operator managing 3M+ sq ft, in-house management." The flagship engagement is the lead consulting bullet because it shows multi-system architecture at real enterprise scale.
- **Lead with the buyer's mirror.** Tailor the framing so the hiring manager thinks "this person already works for someone like us." For a family-office/property/construction buyer, foreground the family-office real-estate engagement and CFO-level partnership.
- **Summary conveys breadth, not a tool list.** Do NOT inventory four tools in the summary ("n8n, Gumloop, Cursor, Claude Code"). Tools belong in the Skills section. The summary states what he can do (workflow orchestration, multi-LLM agent systems, production dashboards, API integrations).

## Fixed facts and metrics (use exactly)

- Education: Ithaca College (BS, Sport Management and Legal Studies, 2018); Northeastern University (Data Analytics Certificate, 2019).
- Background: ~6 years at Spectrum Enterprise / Charter as Business Systems Analyst before independent AI consulting in 2025.
- Reusable metrics when relevant: 3M+ sq ft portfolio, multi-system integration, ~2 hours/day of manual CFO work eliminated by the bank-deposit→QuickBooks workflow, 70%+ routing accuracy on AgentGuard.
- Key projects to draw from: AgentGuard (live at agentguard-delta.vercel.app), Nash-Satoshi Oracle (4-LLM ensemble), Eve (autonomous infra on OpenClaw, 40+ scheduled jobs, Telegram control, Next.js mission control), Vista (App Store consumer app).

## Structure

Two pages. Sections in order: Summary, Independent Consulting (lead bullet = the family-office engagement, listing the workflows by function and the stack), Earlier Experience (Spectrum/Charter), Skills (grouped: AI Automation & Orchestration / AI Models & APIs / Technical / Documentation & Process / Business Operations), Key Projects, Education.

## Output mechanics

- Build the .docx per the `docx` skill. Two-page target — cut the weakest bullets if it overflows.
- Run the docx validator and an em-dash check before presenting (JT dislikes stray em dashes leaking from generated prose).
- Name the file by target, e.g. `jt-somwaru-resume-<company>.docx`.
