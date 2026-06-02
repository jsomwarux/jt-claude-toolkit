---
name: opportunity-research
description: Research a company or vertical and rank its top AI automation opportunities. Use this skill whenever the user names a prospective or existing client (or an industry) and wants to know what to automate, where the highest-value automation opportunities are, what to pitch, or how to scope an engagement. Always use this at the start of a new client engagement or when evaluating a niche (construction, property management, insurance, wholesale distribution, real estate, skilled trades, etc.). Produces a ranked, demo-able opportunity list.
---

# Opportunity Research

Turn a company or vertical into a ranked, pitchable list of AI automation opportunities. The goal is a shortlist JT can demo and quote, not an exhaustive consulting report.

## Workflow

1. Research the target. Use web search for the company's site and the vertical's known pain points. Identify the business model (often there are 2+ revenue lines — handle each separately). Note where work is manual, where tribal knowledge lives, and where money leaks.
2. Identify candidate automations grounded in that specific business, not generic ideas.
3. Rank by impact × feasibility (see scoring).
4. Output the shortlist in the format below.

## Output format

```
# <Company> — Automation Opportunities

## Business Snapshot
<2–3 sentences: what they do, the distinct business lines, where the manual pain is.>

## Top Opportunities (ranked)
### 1. <Opportunity name>
- The gap: <the manual/painful status quo>
- The automation: <what gets built>
- Impact: <hours saved / errors removed / revenue protected>
- Feasibility: <data availability, integration difficulty, demo-ability>
- Ensemble fit: <single-LLM or 4-LLM ensemble, one line why>
- Indicative price band: <$ range>

### 2. ...
```

When the business has multiple lines, give a balanced split (e.g. "3 for hotel ops, 3 for co-living").

## Scoring lenses

- **Impact**: how much time/money/risk it removes, and how visibly. Prefer pains the owner feels daily (e.g. "the first 2 hours of every morning").
- **Feasibility**: is the input data accessible and clean? How many systems must integrate? Can it be demoed with synthetic test data before real data?
- **Demo-ability**: every opportunity must be demonstrable with test data you can fabricate, because JT pitches with a working demo before touching client data. Down-rank anything that can't be shown without production access.
- **Defensibility**: flag where a 4-LLM ensemble adds a real audit trail (insurance, risk, compliance) versus where it's just marketing dressing on a deterministic calc.

## Common vertical starting points

Use these as priors, then tailor to the actual company:
- Real estate / property mgmt: lease abstraction, maintenance triage, owner reporting, rent delinquency outreach, insurance/COI tracking, bank reconciliation.
- Insurance: FNOL/claims intake triage, coverage-gap analysis, underwriting extraction, leakage detection, renewal automation. (Strong ensemble fit.)
- Construction / trades: RFI/submittal drafting, change-order backup, schedule-slip early warning, bid risk scoring, permit compilation.
- Wholesale distribution: quote intake parsing from unstructured inputs, product substitution engine, RAG product copilot, vendor reliability scoring.
