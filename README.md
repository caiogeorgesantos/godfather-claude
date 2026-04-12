# 🤵 buildflow

> *"Build like a team of 50. Work like a team of one."*

**Harness engineering framework for building products with AI agents — from zero to infinity.**

---

## What it is

buildflow is a harness engineering framework for solo founders building products with Claude.
It covers the complete lifecycle — from first idea to monitoring and continuous evolution.

Defines **how to work** — not what to work on.

The core insight: **the model is not the hard part — the harness is.** The constraints, feedback loops, sensors, and lifecycle management around the AI agent determine whether output is reliable or unpredictable. buildflow is that harness.

Solves the real problems of AI-assisted development: agents that go off the rails, code that breaks other code, context that's lost between sessions, incomplete deliveries, and products that go to production without quality.

---

## How it works in 30 seconds

1. Copy `BUILDFLOW-PROJETO.md` to the project root as `CLAUDE.md`
2. Fill in project identity (10 lines)
3. For new projects, run `BUILDFLOW-PESQUISA.md` in Claude.ai (interview → research → spec)
4. Install hooks from `BUILDFLOW-HOOKS.md` and create `scripts/init.sh`
5. Configure computational sensors (linter + typecheck + tests)
6. Open Claude Code — guardrails active automatically

Claude Code reads `CLAUDE.md` every session. Hooks enforce constraints deterministically. Sensors verify automatically. You steer the harness, not the agent directly.

---

## The 4 pillars

buildflow implements the four pillars of harness engineering:

```
┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐
│  CONSTRAIN  │  │   INFORM    │  │   VERIFY    │  │   CORRECT   │
│             │  │             │  │             │  │             │
│ Golden Rule │  │  CLAUDE.md  │  │   Linter    │  │ Self-repair │
│   Hook 1    │  │  SPEC.md    │  │  Typecheck  │  │  Handoff    │
│ Module Plan │  │  ARCH.md    │  │   Tests     │  │  progress   │
│  .claudeignore │  init.sh   │  │  Review     │  │   Radar     │
└─────────────┘  └─────────────┘  └─────────────┘  └─────────────┘
```

---

## The 11 Phases — from zero to infinity

```
PHASE 0  — IDEA           Documented hypothesis
PHASE 1  — RESEARCH       Validated report with real data
PHASE 2  — VALIDATION     Go/no-go with real market
PHASE 3  — SPECIFICATION  SPEC.md approved
PHASE 4  — BRAND          Brand identity
PHASE 5  — PLANNING       ARCH.md approved
PHASE 6  — DESIGN         Approved mockups
PHASE 7  — EXECUTION      Product built, audited, tested
PHASE 8  — LAUNCH         Product in production
PHASE 9  — MONITORING     Continuous intelligence
PHASE 10 — EVOLUTION      Restarts at Phase 3 or 4 with real data
```

The product never stops. Phase 10 feeds Phase 3 with real-world data.

---

## Framework files

| File | Function | When to use |
|------|----------|-------------|
| `BUILDFLOW-PROJETO.md` | Template → becomes the project's CLAUDE.md | Every project |
| `BUILDFLOW.md` | Principles, phases, harness model | On-demand reference |
| `BUILDFLOW-PESQUISA.md` | Interview + research (Phase 1) | Before each project |
| `BUILDFLOW-DEV.md` | Development protocol (Phase 7) | When building |
| `BUILDFLOW-HOOKS.md` | Deterministic hooks and sensors | Project setup |

---

## What makes buildflow different

|  | Other frameworks | buildflow |
|--|------------------|-----------|
| Model | Prompt engineering | Harness engineering (4 pillars) |
| Lifecycle | Execution only | 11 phases — idea to infinity |
| Pre-project research | Absent | Mandatory with structured interview |
| Guardrails | Absent or prompt-based | Deterministic hooks (code, not suggestions) |
| Verification | Manual review | Automated sensors + human review |
| Self-repair | Absent | Sensor → fix → retry loop (max 3) |
| Session continuity | Varies | Structured handoff (init.sh + progress.md) |
| Market validation | Absent | Phase 2 before building |
| Architecture | Implicit | Explicit — ARCH.md before code |
| Module scope | Absent | Mandatory Module Plan — exact file list |
| Code review | Rare | Mandatory in separate session |
| Context budget | Ignored | Design principle (120-line CLAUDE.md) |
| Harness evolution | Static | Weekly steering loop (efficiency radar) |
| Human/AI split | Implicit | Explicit — who does what |

---

## Golden Rule

```
REVERSIBLE   → execute + log + report
IRREVERSIBLE → stop + describe + wait for approval
```

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

## Author

**Caio George Santos**

---

## License

MIT — free to use, modify, and distribute with attribution.

Copyright (c) 2026 Caio George Santos

*Build like a team of 50. Work like a team of one.* 🤵
