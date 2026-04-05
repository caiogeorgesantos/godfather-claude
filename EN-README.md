# 🤵 buildflow

> *"Build like a team of 50. Work like a team of one."*

**A complete framework for building products with AI agents — from idea to infinity.**

**Autonomous · Token-efficient · Secure · Scalable**

---

## What is buildflow

buildflow is an operational framework for building products with AI agents on Claude Code. It covers the entire product lifecycle — from the first idea to continuous monitoring and evolution.

It defines **how to work** — not what to work on. Each project defines its own scope.

It solves the core problems of AI-assisted development: no structure before building, agents that go off-track, code that breaks other code, squads with no memory, and products that ship without quality.

---

## The Golden Rule

```
REVERSIBLE   → execute + log in MEMORY.md + report in session summary
IRREVERSIBLE → stop + describe intended action + wait for Director approval
```

---

## The 11 Phases — From Idea to Infinity

```
PHASE 0  — IDEA
          Structured brainstorm. Turns a raw thought into a
          testable hypothesis worth researching.
          Tool: claude.ai
          Deliverable: hypothesis document

PHASE 1  — RESEARCH
          Deep research squad running in parallel.
          Validates hypotheses with real data.
          Tool: claude.ai (research squad)
          Deliverable: validated research report
          Doc: EN-BUILDFLOW-RESEARCH.md ✅

PHASE 2  — VALIDATION
          Tests with real market before building anything.
          Landing pages, interviews, pre-sales, prototypes.
          Tool: claude.ai + external tools
          Deliverable: go / no-go with real data

PHASE 3  — SPECIFICATION
          Translates validated idea into unambiguous product spec.
          Eliminates what the AI decides when you don't say.
          Tool: claude.ai
          Deliverable: SPEC.md approved by Director

PHASE 4  — BRAND
          Builds brand identity using validated research.
          Who the brand is, how it speaks, what it never does.
          Tool: claude.ai
          Deliverable: brand guide

PHASE 5  — PLANNING
          Defines how to build: architecture, phases, dependencies.
          Tool: claude.ai + Claude Code
          Deliverable: ARCH.md approved by Director

PHASE 6  — DESIGN
          UX, UI, accessibility, design system, mockups.
          No screen gets coded without an approved mockup.
          Tool: claude.ai + v0.dev
          Deliverable: approved mockups

PHASE 7  — EXECUTION
          Builds the product module by module.
          Architect → Developer → Auditor → QA → Security.
          Tool: Claude Code
          Deliverable: built, audited, tested product
          Doc: EN-BUILDFLOW-DEV.md ✅

PHASE 8  — LAUNCH
          Controlled deploy to production.
          Checklist, monitoring, rollback plan.
          Tool: Claude Code + external tools
          Deliverable: product in production

PHASE 9  — MONITORING
          Continuous intelligence on market, competition,
          technology, user behavior, and delivery quality.
          Tool: claude.ai
          Deliverable: periodic intelligence report

PHASE 10 — EVOLUTION
          Transforms monitoring into product decisions.
          Restarts the cycle at Phase 3 or 4 with real data.
          Tool: claude.ai + Claude Code
          Deliverable: approved evolution decision + briefing
```

The product never stops. Phase 10 feeds back into Phase 3 or 4 — always informed by real data from monitoring.

---

## Framework modules

| Module | File | Phase | Status |
|--------|------|-------|--------|
| Global | `EN-BUILDFLOW-GLOBAL.md` | All | ✅ |
| Orchestrator | `EN-BUILDFLOW-ORCHESTRATOR.md` | All | ✅ |
| Agent | `EN-BUILDFLOW-AGENT.md` | All | ✅ |
| Project Template | `EN-BUILDFLOW-PROJECT-TEMPLATE.md` | All | ✅ |
| Research | `EN-BUILDFLOW-RESEARCH.md` | Phase 1 | ✅ |
| Dev | `EN-BUILDFLOW-DEV.md` | Phase 7 | ✅ |
| Idea | `BUILDFLOW-IDEA.md` | Phase 0 | ⏳ build when needed |
| Validate | `BUILDFLOW-VALIDATE.md` | Phase 2 | ⏳ build when needed |
| Spec | `BUILDFLOW-SPEC.md` | Phase 3 | ⏳ build when needed |
| Brand | `BUILDFLOW-BRAND.md` | Phase 4 | ⏳ build when needed |
| Plan | `BUILDFLOW-PLAN.md` | Phase 5 | ⏳ build when needed |
| Design | `BUILDFLOW-DESIGN.md` | Phase 6 | ⏳ build when needed |
| Launch | `BUILDFLOW-LAUNCH.md` | Phase 8 | ⏳ build when needed |
| Monitor | `BUILDFLOW-MONITOR.md` | Phase 9 | ⏳ build when needed |
| Evolve | `BUILDFLOW-EVOLVE.md` | Phase 10 | ⏳ build when needed |

---

## Folder structure

```
~/Documents/Claude/
├── EN-BUILDFLOW-GLOBAL.md
├── EN-BUILDFLOW-ORCHESTRATOR.md
├── EN-BUILDFLOW-AGENT.md
├── EN-BUILDFLOW-RESEARCH.md
├── EN-BUILDFLOW-DEV.md
│
└── your-project/
    ├── CLAUDE.md                  → Orchestrator identity
    ├── BUILDFLOW-PROJECT.md       → Agent map and project flow
    ├── SPEC.md                    → What gets built (Phase 3)
    ├── ARCH.md                    → How it gets built (Phase 5)
    ├── MEMORY.md                  → Living memory
    ├── DECISIONS.md               → Permanent decision log
    ├── STATUS.md                  → Squad control panel
    ├── _briefings/
    ├── _templates/
    └── agent-name/
        ├── CLAUDE.md
        ├── MEMORY.md
        └── DECISIONS.md
```

---

## How EN-BUILDFLOW-DEV.md works (Phase 7)

The most mature module — built from real project experience.

### The development flow per module

```
1. Architect defines ARCH.md
         ↓
2. Director approves ARCH.md
         ↓
3. Architect runs /plan for each module
   → lists exact files to create, modify, reuse
         ↓
4. Director approves Module Plan
         ↓
5. Developer builds using specialized writers:
   component-writer · action-writer · hook-writer
   integration-writer · model-writer · route-writer · test-writer
         ↓
6. Code Auditor reviews — cross-references against Module Plan
         ↓
7. QA Tester tests happy path + edge cases + failure states
         ↓
8. Merge branch to main
         ↓
9. Repeat for next module
         ↓
10. Security Reviewer clears for production
         ↓
11. Ship
```

### Quality Gates — nothing passes without these

| Gate | Who approves | What blocks |
|------|-------------|-------------|
| SPEC.md approved | Director | Nothing gets built |
| ARCH.md approved | Director | No code gets written |
| Module Plan approved | Director | Developer doesn't start |
| Module audited | Code Auditor | Module doesn't go to QA |
| Module tested | QA Tester | Module doesn't merge |
| Security cleared | Security Reviewer | Nothing goes to production |

---

## Installation

**Step 1** — Save all `.md` files to `~/Documents/Claude/`

**Step 2** — For each project, copy `EN-BUILDFLOW-PROJECT-TEMPLATE.md` to the project root and rename it `BUILDFLOW-PROJECT.md`

**Step 3** — Add this block to your Orchestrator's `CLAUDE.md`:
```markdown
## Mandatory reading
Before any action, read in this order:
1. ~/Documents/Claude/EN-BUILDFLOW-GLOBAL.md
2. ~/Documents/Claude/EN-BUILDFLOW-ORCHESTRATOR.md
3. ./BUILDFLOW-PROJECT.md
```

**Step 4** — Add this block to each agent's `CLAUDE.md`:
```markdown
## Mandatory reading
Before any action, read in this order:
1. ~/Documents/Claude/EN-BUILDFLOW-GLOBAL.md
2. ~/Documents/Claude/EN-BUILDFLOW-AGENT.md
3. ./BUILDFLOW-PROJECT.md
```

**Step 5** — For new projects, start with BUILDFLOW-RESEARCH. Fill the Pre-Project Form. Run the research squad on claude.ai. Then move through the phases in order.

---

## What makes buildflow different

| Feature | Other frameworks | buildflow |
|---------|-----------------|-----------------|
| Lifecycle coverage | Execution only | Idea to infinity — 11 phases |
| Pre-project research | Absent | Mandatory — Phase 1 |
| Market validation | Absent | Phase 2 before building |
| Brand as a phase | Absent | Phase 4 — after validation |
| Architecture phase | Implicit | Explicit — ARCH.md before code |
| Module planning | Absent | /plan per module — exact files listed |
| Specialized writers | Absent | 7 writer types per file category |
| Git branching | Rarely enforced | Branch per module — mandatory |
| Code audit | Rare | Mandatory after every module |
| QA testing | Optional | Mandatory after every audit |
| Security review | Rare | Mandatory before every production deploy |
| Cross-session memory | Varies | MEMORY.md + DECISIONS.md standard |
| Monitoring & evolution | Absent | Phases 9 and 10 — continuous loop |

---

## Research basis

buildflow was built from:
- Anthropic Engineering — How we built our multi-agent research system (2025)
- Anthropic — Claude Code Best Practices (2026)
- shanraisshan/claude-code-best-practice — GitHub (2026)
- Addy Osmani — How to write a good spec for AI agents (2026)
- Deborah Folloni — Meu novo workflow Claude Code + Epic CLI (2026)
- oh-my-claudecode, Everything-Claude-Code, SuperClaude
- Real project experience — SEO, systems, and product development (2026)

---

## Author

**Caio George Santos**

---

## License

MIT — free to use, modify, and distribute with attribution.

Copyright (c) 2026 Caio George Santos

---

*Build like a team of 50. Work like a team of one.* 🤵
