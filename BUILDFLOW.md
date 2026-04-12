# 🤵 BUILDFLOW
# Harness engineering framework for building products with AI agents.
# Version: 4.0 · 2026 · Caio George Santos · MIT License
# This document is reference. Not read automatically every session.
# The operational document is each project's BUILDFLOW-PROJETO.md (→ CLAUDE.md).

> *"Build like a team of 50. Work like a team of one."*

---

## What it is

Operational harness engineering framework for solo founders building products with Claude.
Defines **how to work** — not what to work on.
Each project has its own BUILDFLOW-PROJETO.md that defines what to work on.

**Agent = Model + Harness.** The model is the engine. The harness is the steering, brakes, and dashboard. Without a harness, even the most powerful model produces unreliable results.

---

## Golden Rule

```
REVERSIBLE   → execute + log to ESTADO + report in summary
IRREVERSIBLE → stop + describe the action + wait for Director approval
```

---

## The Harness Model — 4 pillars

Everything in the framework serves one of four functions:

| Pillar | Function | BUILDFLOW implementation |
|--------|----------|--------------------------|
| **Constrain** | Prevent the agent from doing wrong things | Golden Rule, Hook 1 (irreversible action gate), Hook 5 (filesystem sandbox), Module Plan |
| **Inform** | Give the agent the right context | CLAUDE.md, SPEC.md, ARCH.md, init.sh, Skills, Module Plan |
| **Verify** | Check that the agent did it correctly | Computational sensors (lint, test, typecheck), inferential sensors (review agent), Quality Gates |
| **Correct** | Fix when things go wrong | Self-repair loop, handoff artifacts, weekly efficiency radar, cleanup tasks |

---

## Guides and sensors

Borrowed from Thoughtworks' harness engineering model. Two types of controls:

**Guides (feedforward)** — steer the agent *before* it acts:
- CLAUDE.md, SPEC.md, ARCH.md → inform intent and constraints
- Module Plan → scope exactly which files to touch
- Skills → specialized knowledge loaded on demand
- init.sh → dynamic context injected at session start

**Sensors (feedback)** — observe *after* the agent acts and enable self-correction:
- **Computational** (deterministic, fast, cheap): linter, typecheck, tests, dep-cruiser, structural tests
- **Inferential** (semantic, slower, expensive): review agent in separate session, LLM-as-judge

**The steering loop**: whenever an issue happens more than once, improve the guides or sensors to prevent it from recurring. The human steers the harness, not the agent directly.

---

## The 11 Phases

| Phase | Name | Where it runs | Deliverable |
|-------|------|---------------|-------------|
| 0 | IDEA | Claude.ai | Documented hypothesis |
| 1 | RESEARCH | Claude.ai | Validated report (see BUILDFLOW-PESQUISA.md) |
| 2 | VALIDATION | Claude.ai + external | Go/no-go with real data |
| 3 | SPECIFICATION | Claude.ai | SPEC.md approved |
| 4 | BRAND | Claude.ai | Brand guide |
| 5 | PLANNING | Claude.ai + Code | ARCH.md approved |
| 6 | DESIGN | Claude.ai + v0.dev | Mockups approved |
| 7 | EXECUTION | Claude Code | Product built (see BUILDFLOW-DEV.md) |
| 8 | LAUNCH | Claude Code + external | Product in production |
| 9 | MONITORING | Claude.ai | Intelligence report |
| 10 | EVOLUTION | Claude.ai + Code | Evolution decision → restarts at Phase 3 or 4 |

The product never stops. Phase 10 feeds Phase 3 or 4 with real-world data.

---

## Where to do each type of task

| Task | Tool | Why |
|------|------|-----|
| Strategy, planning, brainstorming | **Claude.ai (Projects)** | Memory across sessions, web search, integrations |
| Deep research, market analysis | **Claude.ai (Deep Research)** | Automated web research, multi-source synthesis |
| Development, automation, deploys | **Claude Code** | Terminal access, codebase, command execution |
| Complex documents (.docx, .pptx, .xlsx) | **Claude Cowork** | File creation skills, local file access |
| File organization, desktop tasks | **Claude Cowork** | Filesystem access, scheduled tasks |
| Recurring/scheduled tasks | **Claude Cowork (Scheduled Tasks)** | Runs even without you present |
| Study and learning consolidation | **Claude.ai (Projects)** or **NotebookLM** | Persistent context per topic |

Rule: don't switch tools to avoid switching. Switch when the task demands it.

---

## AI model — when to use each one

| Model | Relative cost | When to use |
|-------|---------------|-------------|
| **Haiku** | $ | Research, classification, simple tasks, exploration sub-agents |
| **Sonnet** | $$ | 80% of daily work: code, documents, analysis, implementation |
| **Opus** | $$$$$ | Architectural decisions, complex reviews, Agent Teams, deep reasoning |

Rule: start with Sonnet. Only escalate to Opus when Sonnet results are genuinely insufficient.

---

## Division of responsibilities

### The AI does autonomously (every session, every task):
- Interview before complex tasks
- Choose the appropriate model for the task
- Run init.sh at session start (if it exists)
- Verify completeness before declaring "done"
- Run computational sensors before declaring "done"
- Ask for clarification when the request is ambiguous
- Update ESTADO at session end
- Write handoff artifact at session end
- Alert when context is degrading (>50%)
- Don't over-engineer (follow only the requested scope)
- Search for existing code before creating new

### The Director does (human decisions):
- Approve specs and architectures before execution
- Final review of critical deliverables
- Business decisions (prioritization, go/no-go, pricing)
- Approve spending (deploys, paid APIs, external services)
- Decide when to escalate to Agent Teams
- Define scope and intent for each task
- Steer the harness (improve guides and sensors when issues recur)

### The AI suggests, Director decides:
- When to start a new session (AI alerts, Director decides)
- When to escalate complexity (AI recommends, Director approves)
- When a project needs more context/skills

---

## Context engineering principles

1. **Short, focused sessions.** One task per session. Don't reuse sessions for different tasks.
2. **Lean CLAUDE.md.** BUILDFLOW-PROJETO.md must be under 120 lines. If it grows beyond that, move knowledge to Skills.
3. **Skills > CLAUDE.md** for specialized knowledge. Skills load on demand, CLAUDE.md loads every session.
4. **`/compact` at 50%.** Don't wait for auto-compact at 95%. When compacting, state what to preserve.
5. **`/clear` to switch tasks.** Don't mix planning and execution in the same session.
6. **`.claudeignore`** to exclude node_modules, dist, lock files, build artifacts.
7. **Specific prompts.** "Fix auth bug in src/auth.js" costs fewer tokens than "fix the bug."
8. **If the agent contradicts previous decisions:** context has degraded. Start a new session.
9. **init.sh runs first.** Every session begins by reading progress and running the bootstrap script.
10. **Cost awareness.** Opus costs ~5x Sonnet. Agent Teams consume 3-7x single session. Before escalating to Opus or Agent Teams, state the reason. If a session runs over 30 minutes on Opus, pause and ask if the Director wants to continue.

---

## Installation

1. Copy `BUILDFLOW-PROJETO.md` to each project root and rename to `CLAUDE.md`
2. Fill in project identity, constraints, and business context
3. For new projects, start with `BUILDFLOW-PESQUISA.md` in Claude.ai
4. Install hooks from `BUILDFLOW-HOOKS.md` into `.claude/settings.json`
5. Create `scripts/init.sh` following the template in BUILDFLOW-DEV.md
6. Configure computational sensors (linter + tests) for the project's stack
7. Keep `BUILDFLOW.md`, `BUILDFLOW-PESQUISA.md`, and `BUILDFLOW-DEV.md` in `~/Documents/Claude/` as reference

---

## Research base

Built from:
- Anthropic — Effective Harnesses for Long-Running Agents (2025)
- Anthropic — Harness Design for Long-Running Application Development (2026)
- Anthropic — Context Engineering for AI Agents (2025-2026)
- OpenAI — Harness Engineering: Leveraging Codex in an Agent-First World (2026)
- Thoughtworks / Birgitta Böckeler — Harness Engineering for Coding Agent Users (2026)
- Red Hat — Harness Engineering: Structured Workflows for AI-Assisted Development (2026)
- Real project experience — SEO, legaltech, SaaS, product development (2025-2026)

---

## License

MIT — free to use, modify, and distribute with attribution.
Copyright (c) 2026 Caio George Santos

*Build like a team of 50. Work like a team of one.* 🤵
