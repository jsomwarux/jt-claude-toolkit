---
name: proposal-pdf
description: Generate a branded client proposal PDF in JT's exact house style. Use this skill whenever the user asks for a proposal, a scope-of-work document, a client quote, an engagement proposal, a SOW, or any priced client-facing deliverable as a PDF — even if they don't say the word "proposal." Always use this when a deliverable lists use cases with prices and a total. Produces a weasyprint PDF matching the established blue-accent layout so there is zero design back-and-forth.
---

# Proposal PDF

Generate a client proposal PDF that matches JT's established house style on the first pass. The whole point of this skill is to eliminate design iteration — the layout is already decided, so spend effort on the content, not the styling.

## Workflow

1. Collect the content. You need: proposal title, subtitle, client name + contact, an overview paragraph, a list of use cases (each with a title, price, 1–2 sentence description, and an optional italic recommendation note), the pricing line items, the total, and a timeline paragraph. If the user hasn't given a piece, ask once for the missing fields together — don't drip-feed questions.
2. Copy the template to a working file: `cp "${CLAUDE_PLUGIN_ROOT}/skills/proposal-pdf/assets/proposal_template.html" /tmp/proposal.html` (in Claude.ai use `/home/claude/proposal.html`).
3. Fill every `{{PLACEHOLDER}}`. Duplicate the `.use-case` block once per use case and the pricing `<tr>` row once per line item. Footer is `JT Somwaru | jtsomwaru.com` unless told otherwise.
4. Render: `python3 -c "from weasyprint import HTML; HTML('/tmp/proposal.html').write_pdf('<output>.pdf')"`. Install weasyprint with `pip install weasyprint --break-system-packages` if missing.
5. Present the PDF.

## Non-negotiable design tokens

Never alter these unless the user explicitly asks:

- **Split header**: title + subtitle on the left, "Prepared for / client / contact / date" right-aligned on the right.
- **Accent line**: 4px gradient bar, `#4A6CF7` → `#6B8AFF`, directly under the header.
- **Section labels**: uppercase, letter-spaced, color `#4A6CF7`.
- **Use cases**: bold dark title on the left, bold blue price right-aligned on the same line; recommendation notes in blue italic.
- **Pricing table**: line items with right-aligned amounts; the Total row has a 2px blue top border and a blue amount.
- Body font Helvetica/Arial, ~10.5pt, dark slate text (`#2D3748`), Letter size.

## Pricing discipline

- Show each use case price next to its title AND repeat it as a line item in the Investment table. The two must reconcile to the Total.
- Phase work explicitly when an engagement is staged (e.g. "Phase 1: Legal Rent Only"). Don't bury phasing in prose.
- If the user gives a monthly retainer or support fee, list it as a separate line, not folded into the implementation total.

## Quality check before presenting

Open the PDF and confirm: the accent line renders as a gradient (not a flat bar), prices are right-aligned and reconcile to the total, no `{{PLACEHOLDER}}` text remains, and the footer shows on every page. If a flat/colorless render appears, weasyprint is fine but verify the gradient CSS wasn't stripped.
