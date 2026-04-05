# 🤵 buildflow
# Module: RESEARCH
# Version: 1.0 · 2026
# Use: Before any project starts. No exceptions.

> *"Never make a decision based on estimates when data exists."*

---

## What this module is

BUILDFLOW-RESEARCH is the protocol for Phase 1 of the buildflow framework.
It runs entirely on claude.ai — not Claude Code.
It ends with one deliverable: a validated research report per area.
The research report feeds Phase 3 (Specification) where SPEC.md is produced.
Nothing gets specified until the research report is complete and reviewed.

Framework phases for reference:
- Phase 0 — IDEA · Phase 1 — RESEARCH (this module) · Phase 2 — VALIDATION
- Phase 3 — SPEC · Phase 4 — BRAND · Phase 5 — PLAN · Phase 6 — DESIGN
- Phase 7 — EXECUTION · Phase 8 — LAUNCH · Phase 9 — MONITORING · Phase 10 — EVOLUTION

---

## The Pre-Project Form

This form is your guardrail. Fill it before talking to any AI.
It forces you to think at the maximum level from the start.
Incomplete answers = incomplete research = broken product.

---

### BLOCK 1 — The Vision

```
Project name:
One sentence describing what it is:
One sentence describing what problem it solves:
Who uses it (be specific — not "people", but who exactly):
What does success look like in 6 months (concrete metric):
What does failure look like (what would make you abandon it):
```

### BLOCK 2 — The Business

```
How does this product make money:
Is there a secondary revenue model:
What is the pricing model (subscription / one-time / freemium / B2B):
Who pays (the user, a third party, advertisers):
What existing data do you have that is relevant
(leads database, sales history, Google Ads data, GSC, CRM, other):
What conversion data exists (what converts, what doesn't):
```

### BLOCK 3 — The Market

```
Who are the 3 main competitors (name them, don't say "I don't know"):
What do competitors do well that you need to match:
What do competitors do poorly that is your opportunity:
Is there a global reference (outside Brazil) that does this well:
What is the realistic market size (don't estimate — if you don't know, say so):
```

### BLOCK 4 — The Brand

```
Is there a brand guide / style guide: (yes/no — if yes, attach)
What is the brand's tone of voice:
What does the brand absolutely NOT do or say:
What visual references inspire you (sites, apps, products):
Does a logo exist: (yes/no)
Does a color palette exist: (yes/no)
```

### BLOCK 5 — Technical Context

```
Does an existing system need to integrate with this: (yes/no — if yes, describe)
Is there an existing database: (yes/no — if yes, what is in it)
Is there an existing codebase: (yes/no — if yes, what language/framework)
Is there a domain already: (yes/no)
Is there hosting already: (yes/no — if yes, where)
What is the budget for infrastructure per month (approximate):
```

### BLOCK 6 — Constraints

```
What is the launch deadline (if any):
What cannot change under any circumstances:
What requires legal/compliance/regulatory review:
Who needs to approve before anything goes live:
What is the content review process (who validates before publishing):
```

### BLOCK 7 — Quality Standard

```
What is the global reference for quality you want to match or beat:
What would make you say "this is the best in Brazil":
What would make you say "this is the best in the world":
Are you willing to delay launch to reach this quality level: (yes/no)
```

---

## Mandatory Rules Before Starting Research

Before any research IA starts working, confirm:

- [ ] All 7 blocks of the form are filled
- [ ] All existing data has been shared (GSC, Supabase, Ads, CRM)
- [ ] Brand guide has been read (if it exists)
- [ ] Conversion data has been analyzed (if it exists)
- [ ] Real market volumes will be validated — no estimates accepted

**If any of these is missing: stop. Get the information. Then start.**

---

## The Research Squad — claude.ai Projects

Create one claude.ai Project per product being researched.
Upload the filled form as the project's knowledge base.
Each IA below is a separate chat within that project.

### Standard Research Squad

| IA | Role | Delivers |
|----|------|----------|
| IA 1 — Market Intelligence | Players, benchmarks, trends, gaps | market-intelligence.md |
| IA 2 — User & Conversion | Who converts, why, what blocks them | user-conversion.md |
| IA 3 — Competitor Analysis | Deep analysis of top 3-5 competitors | competitor-analysis.md |
| IA 4 — Technical Research | Stack options, risks, integrations | technical-research.md |
| IA 5 — Business Model | Revenue models, pricing, monetization | business-model.md |
| IA 6 — Content & Brand | Content strategy, tone, structure | content-brand.md |
| IA Consolidator | Synthesizes all outputs into SPEC.md | SPEC.md |

### Rules for Research IAs

- Each IA reads the filled form before starting
- Each IA validates real data before any recommendation
- Estimates are flagged explicitly — never presented as fact
- Each IA delivers its output as a file, not just a chat response
- No IA starts coding or specifying solutions — only researching

### Briefing Template for Each Research IA

```
You are a world-class expert in [domain].
Your mission: research [specific topic] for the following project.

Read the Pre-Project Form attached to this project before anything else.

Research requirements:
- Go deep. Read full articles, not summaries.
- Validate all numbers with real sources.
- Flag anything that is an estimate, not a fact.
- Focus on what is actionable, not theoretical.

Mandatory sources to consult:
- [list specific URLs, databases, or tools relevant to the domain]

Output:
- Save as [filename].md in this project
- Structure: findings → implications → recommendations
- Every recommendation must be justified with data

Do NOT start writing code or specifications.
Do NOT make decisions — surface findings for the Consolidator.
```

---

## The Consolidator IA

After all research IAs deliver their outputs, the Consolidator runs.
The Consolidator synthesizes everything into a research report — not SPEC.md.
SPEC.md is produced in Phase 3 (Specification), using this report as input.

Briefing:
```
You are the Consolidator. Read all research outputs in this project.
Your mission: produce a consolidated research report that will feed
the Specification phase (Phase 3) of the buildflow framework.

The consolidated report must contain:
1. Market summary — key players, gaps, opportunities validated with data
2. User profile — who converts, why, what blocks them
3. Competitor analysis — what they do well, what they don't, our gaps
4. Business model — validated revenue options and pricing benchmarks
5. Technical landscape — stack options, risks, integrations available
6. Content and brand signals — language users use, tone that resonates
7. Key decisions pending — what still needs resolution before specification
8. Risk log — what could go wrong and how to mitigate

Rules:
- Every finding must be traceable to a research output
- No estimates — only validated data
- No assumptions — flag unknowns explicitly
- Flag contradictions between research outputs
- Maximum 400 lines — if it needs more, split by area

When complete, present the report for Director review.
The Director will use this to move to Phase 2 (Validation) or
directly to Phase 3 (Specification) if validation is not needed.
```

---

## Quality Criteria for Research Delivery

A research output is approved when:
- Based on real data, not estimates
- Every recommendation has a justification
- No contradictions with other research outputs
- Actionable — not just theoretical
- Ready to inform SPEC.md directly

A research output is rejected when:
- Uses estimates presented as facts
- Contradicts data from other outputs
- Is superficial (surface-level findings only)
- Cannot be directly used to write SPEC.md

---

## The Handoff to Next Phase

Research ends when:
- [ ] All research IAs have delivered their outputs
- [ ] Consolidated research report has been produced
- [ ] Director has reviewed and approved the research report
- [ ] Key decisions pending have been noted for Phase 2 or Phase 3

The consolidated research report goes into the claude.ai project knowledge base.
It feeds Phase 2 (Validation) or Phase 3 (Specification) directly.
SPEC.md is produced in Phase 3 — not here.

---

## Common Mistakes — Learn From Real Projects

**Mistake 1 — Prioritizing without real data**
Estimated volumes led to wrong priorities. Always validate with real tools
before defining what to build first.

**Mistake 2 — Reading the brand guide late**
Brand guide changed the entire architecture when read on day 3.
Read it before any structure is defined.

**Mistake 3 — Ignoring existing conversion data**
Conversion data revealed that some content categories convert 0%.
Analyze existing data before planning new content or features.

**Mistake 4 — Briefing research IAs with too much scope**
An overloaded research IA stalls and delivers incomplete output.
Keep each IA focused on one domain. Better to add an extra IA
than to overload one.

**Mistake 5 — Skipping the business model**
Monetization came from the Director, not the research.
The business model must be researched and validated, not assumed.

---

MIT License · Copyright (c) 2026 Caio George Santos
