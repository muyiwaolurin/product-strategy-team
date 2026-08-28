# product-strategy-team

A three-agent team that researches named products on the public web, compares their features and UX, and delivers a competitive-positioning strategy as a single Word document with a feature breakdown matrix.

## Components

**Agents**

- `product-researcher` — sourced product intelligence: features, pricing, packaging, releases, reported gaps. Public web only; every claim cited.
- `ux-evaluator` — UX comparison from docs, demos, and reviews: 6-dimension scorecard plus narrative.
- `strategy-lead` — synthesizes both briefs into a feature matrix, competitive read, positioning statements, and prioritized recommendations.

**Skill**

- `compare-products` — the entry point. Runs researcher and UX evaluator in parallel, then the strategy lead, then builds the .docx.

## Usage

Say something like:

- "Compare features from competitors listed"
- "Run a product comparison of X vs Y and build a strategy"
- "Research competitors A, B, C in the on-call scheduling space"

The skill will confirm the products, focus area, and perspective, then deliver `competitive-strategy-[topic].docx`.

## Setup

No environment variables or external servers required. Uses the session's built-in web search and document tools.
