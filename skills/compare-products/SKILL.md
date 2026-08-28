---
name: compare-products
description: >
  This skill should be used when the user asks to "compare products",
  "run a product comparison", "research competitors", "compare features
  between", "build a competitive strategy", or names two or more products
  and wants research, a feature breakdown, or a positioning strategy.
  It orchestrates the product-researcher, ux-evaluator, and strategy-lead
  agents and delivers a single Word (.docx) strategy document.
metadata:
  version: "0.1.0"
---

# Compare products and build a competitive strategy

Orchestrate a three-agent team to research named products, compare their features and UX, and deliver one Word document containing a competitive-positioning strategy with a feature breakdown.

## Inputs to collect before starting

Confirm with the user (ask only for what is missing from their request):

1. **Products** — two or more named products to compare (e.g., Rootly, incident.io).
2. **Focus area** — the capability domain to compare (e.g., incident workflow features). Default to the whole product only if the user says so.
3. **Perspective** — whose competitive position the strategy serves. Default: the user's own product/company (for PagerDuty users, PagerDuty's competing capability).
4. **Audience** — who reads the doc (default: product and engineering leadership).

## Workflow

### Stage 1 — Parallel research (product-researcher + ux-evaluator)

Launch BOTH agents concurrently in a single message:

- **product-researcher**: pass the product list and focus area. Instruct it to return one sourced research brief per product (features, pricing/packaging, recent releases, positioning, reported gaps).
- **ux-evaluator**: pass the same product list and focus area. Instruct it to return the UX scorecard and narrative comparison.

Both agents research the public web only. Do not begin Stage 2 until both have returned.

### Stage 2 — Synthesis (strategy-lead)

Launch **strategy-lead** with: the focus area, product list, perspective, and the FULL text of both Stage 1 briefs. Instruct it to return the complete strategy report including the feature breakdown matrix.

### Stage 3 — Produce the Word document

1. Read the docx skill (SKILL.md) available in this session to learn the document-building procedure.
2. Build a professional .docx from the strategy-lead report with this structure:
   - Title page: "Competitive strategy: [focus area]", products compared, date, "Prepared for [perspective]".
   - Executive summary.
   - Feature breakdown matrix as a formatted table (Yes/Partial/No/Unknown cells; shade differentiator rows).
   - Competitive read: table stakes, differentiators, white space.
   - UX comparison: scorecard table plus narrative.
   - Positioning statements.
   - Prioritized recommendations table (move, rationale, effort S/M/L).
   - Risks and open questions.
   - Appendix: full source list from both research briefs.
3. Save the document to the outputs folder, named `competitive-strategy-[focus-area-slug].docx`.
4. Present the file to the user and summarize the top three takeaways in two or three sentences.

## Quality rules

- Every factual claim in the document must trace to a source gathered in Stage 1; keep URLs in the appendix.
- Mark unknowns as "Unknown" in the matrix — never guess a competitor capability.
- Keep the executive summary under 200 words and free of hedging filler.
- If the user's request involves external-company confidential material (customer records, contract terms, non-public data), pause and confirm data clearance before processing; public web research on competitors is fine.
