# BUILDFLOW-PESQUISA
# Phase 1 of the buildflow framework. Runs on Claude.ai, not Claude Code.
# Version: 4.0 · 2026

> *"Never make a decision based on estimates when real data exists."*

---

## What it is

Protocol for Phase 1 (Research) of buildflow.
Ends with a validated research report that feeds Phase 3 (Specification/SPEC.md).
Nothing is specified until research is complete and reviewed.

---

## How it works

Research starts with an **interview** — the AI asks, the Director answers.
Then the AI researches and consolidates. The Director reviews and approves.

```
Interview (7 blocks) → Deep research → Consolidated report → Director approval → Phase 3
```

---

## Interview protocol — 7 blocks

The AI must conduct the interview using the blocks below as a guide.
Don't present the entire form at once — go block by block, conversationally.
Accept partial answers. Flag when information is missing but don't block.

### Block 1 — Vision
- What is this project?
- What problem does it solve?
- Who uses it (be specific — not "people", but who exactly)?
- What does success look like in 6 months (concrete metric)?
- What would make you abandon the project?

### Block 2 — Business
- How does this product make money?
- Is there a secondary revenue model?
- What's the pricing model (subscription / one-time / freemium / B2B)?
- Who pays (the user, a third party, advertisers)?
- What existing data is relevant (leads, sales, Ads, CRM, GSC)?
- What conversion data exists (what converts, what doesn't)?

### Block 3 — Market
- Who are the top 3 competitors (name them)?
- What do they do well that you need to match?
- What do they do poorly that is your opportunity?
- Is there a global reference (outside Brazil) that does this well?
- What's the realistic market size (don't estimate — if unknown, say so)?

### Block 4 — Brand
- Does a brand guide / style guide exist?
- What's the tone of voice?
- What does the brand absolutely NOT do or say?
- What visual references inspire (sites, apps, products)?
- Does a logo and color palette exist?

### Block 5 — Technical context
- Is there a system this needs to integrate with?
- Does a database exist? What's in it?
- Does code exist? What language/framework?
- Does a domain and hosting exist?
- What's the monthly infrastructure budget?

### Block 6 — Constraints
- What's the launch deadline?
- What cannot change under any circumstances?
- What requires legal/compliance review?
- Who needs to approve before going live?

### Block 7 — Quality standard
- What global quality reference do you want to match or surpass?
- What would make you say "this is the best in Brazil"?
- What would make you say "this is the best in the world"?
- Are you willing to delay the launch to reach that level?

---

## Rules before researching

Before starting research, confirm:
- [ ] All 7 interview blocks were covered (partial answers ok, as long as flagged)
- [ ] Existing data was shared (GSC, Supabase, Ads, CRM) — if they exist
- [ ] Brand guide was read — if it exists
- [ ] Conversion data was analyzed — if it exists

If critical information is missing: flag it and proceed with what's available. Don't block.

---

## Research

Use Deep Research or manual research to cover:

1. **Market** — players, gaps, opportunities, real size
2. **User** — who converts, why, what blocks them
3. **Competitors** — deep analysis of top 3-5
4. **Business model** — validated revenue options, pricing benchmarks
5. **Technical landscape** — stack options, risks, integrations
6. **Content and brand** — language users use, tone that resonates

Rules:
- Validate numbers with real sources. Explicitly flag what is estimate vs fact.
- Focus on what is actionable, not theoretical.
- Maximum 400 lines in the report. If more is needed, split by area.

---

## Consolidated report

The report must contain:

1. Market summary — validated with data
2. User profile — who converts and why
3. Competitor analysis — strengths, weaknesses, gaps
4. Business model — validated options
5. Technical landscape — recommended stack with justification
6. Content and brand signals
7. **Pending decisions** — what still needs to be resolved before specifying
8. **Risks** — what can go wrong and how to mitigate

Every finding must be traceable. No estimates as facts. No assumptions — flag unknowns.

---

## Handoff to next phase

Research ends when:
- [ ] Consolidated report produced
- [ ] Director reviewed and approved
- [ ] Pending decisions noted for Phase 3

The report goes into the Claude.ai Project as project knowledge.
It directly feeds Phase 3 (Specification) where SPEC.md is produced.

---

## Common mistakes

**Prioritizing without real data.** Estimated volumes lead to wrong priorities. Validate with real tools before defining what to build first.

**Reading the brand guide late.** The brand guide can change the entire architecture. Read it before any structure.

**Ignoring existing conversion data.** Conversion data may reveal that entire categories convert at 0%. Analyze before planning.

**Skipping the business model.** Monetization must be researched and validated, not assumed.

---

MIT License · Copyright (c) 2026 Caio George Santos
