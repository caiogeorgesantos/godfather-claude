# BUILDFLOW-DEV
# Phase 7 of the buildflow framework. Development protocol with Claude Code.
# Version: 4.0 · 2026
# Loaded on demand via @reference, not every session.

> *"A well-built foundation prevents exponential rework."*

---

## Entry criteria — before opening Claude Code

- [ ] SPEC.md exists and was approved by the Director
- [ ] ARCH.md exists and was approved by the Director
- [ ] Stack defined
- [ ] Open questions from SPEC.md resolved
- [ ] Git repository created with main branch
- [ ] BUILDFLOW-PROJETO.md configured as the project's CLAUDE.md
- [ ] Computational sensors configured (linter + typecheck + tests)
- [ ] `scripts/init.sh` created from template below
- [ ] Hooks installed from BUILDFLOW-HOOKS.md

**If any item is missing: don't start. Resolve it first.**

---

## SPEC.md and ARCH.md — new vs existing projects

**New project:** create complete SPEC.md and ARCH.md before any code.

**Existing project:** DON'T duplicate documentation. Create lean wrappers (~100 lines):

```
SPEC.md (wrapper)
- What this product is (2-3 lines)
- Links to existing spec docs
- What is OUT of scope
- Quality criteria
- Gate: Director approves before any module

ARCH.md (wrapper)
- Stack (1 line each)
- Links to existing technical docs
- List of modules in execution order
- Gate: Director approves before any code
```

---

## Harness setup — the foundation

### scripts/init.sh — dynamic context at session start

Every project must have this script. The agent runs it at the start of every session.

```bash
#!/bin/bash
# BUILDFLOW init.sh — bootstraps agent context at session start
# Run: bash scripts/init.sh

echo "=== BUILDFLOW INIT ==="
echo ""

# 1. Where we are
echo "📁 Working directory: $(pwd)"
echo "🌿 Current branch: $(git branch --show-current 2>/dev/null || echo 'not a git repo')"
echo ""

# 2. Recent history
echo "📋 Last 10 commits:"
git log --oneline -10 2>/dev/null || echo "No git history"
echo ""

# 3. Pending changes
echo "📝 Uncommitted changes:"
git status --short 2>/dev/null || echo "Clean"
echo ""

# 4. Open branches
echo "🔀 Open branches:"
git branch --list 'feature/*' 2>/dev/null || echo "No feature branches"
echo ""

# 5. Sensor status (adapt commands to your stack)
echo "🔍 Running sensors..."
# Uncomment and adapt for your stack:
# npx biome check src/ --no-errors-on-unmatched 2>&1 | tail -3
# npx tsc --noEmit 2>&1 | tail -5
# npm test -- --silent 2>&1 | tail -5
echo ""

# 6. Progress file
if [ -f "progress.md" ]; then
  echo "📊 Progress from last session:"
  cat progress.md
else
  echo "📊 No progress.md found (first session or new project)"
fi

echo ""
echo "=== INIT COMPLETE ==="
```

Make it executable: `chmod +x scripts/init.sh`

### Computational sensors — what to configure

Every project must have at minimum:

| Sensor type | What it catches | Example tools |
|-------------|-----------------|---------------|
| **Linter** | Style violations, bad patterns | ESLint, Biome, Ruff, Clippy |
| **Typecheck** | Type errors, missing interfaces | tsc, mypy, cargo check |
| **Tests** | Broken behavior, regressions | Jest, pytest, cargo test |

Optional but recommended:

| Sensor type | What it catches | Example tools |
|-------------|-----------------|---------------|
| **Dependency check** | Circular imports, boundary violations | dep-cruiser, madge |
| **Security scan** | Known vulnerabilities, secrets in code | npm audit, semgrep, gitleaks |
| **Bundle analysis** | Size regressions, unnecessary imports | bundlewatch, webpack-bundle-analyzer |

Configure the exact commands in the CLAUDE.md "Computational sensors" section.

---

## Module Plan — the most important guardrail

Before building any module, produce a Module Plan:

```
MODULE PLAN — [name]
Branch: feature/[module-name]

What it does: [one sentence]

Files to CREATE:
- [path] — [what it contains]

Files to MODIFY:
- [path] — [what changes and why]

Files to REUSE:
- [path] — [how it will be used]

Behaviors:
- Happy path: [what happens when it works]
- Edge cases: [what happens at the limits]
- Errors: [what happens when it fails]

Acceptance criteria:
- [ ] [specific testable criterion]
- [ ] [specific testable criterion]
- [ ] Computational sensors pass (lint + typecheck + tests)
```

**Rule: if a file is not in the plan, don't touch it.** This is the most important rule to prevent rogue AI.

Director approves the Plan before building starts.

---

## The self-repair loop

When computational sensors detect a failure after the agent writes code:

```
Agent writes code
    → Sensors run automatically (lint, typecheck, tests)
    → If ALL PASS → continue
    → If FAIL:
        → Read error output
        → Attempt fix (max 3 attempts)
        → Run sensors again
        → If STILL FAILING after 3 attempts:
            → STOP
            → Report to Director with:
              - What failed
              - What was attempted
              - Error output
              - Hypothesis for root cause
```

This loop is enforced by Hook 3 in BUILDFLOW-HOOKS.md. The agent does NOT declare "done" until sensors pass or the Director is informed.

---

## Quality Gates

| Gate | Who approves | What it blocks |
|------|-------------|----------------|
| SPEC.md approved | Director | Nothing is built |
| ARCH.md approved | Director | No code is written |
| Module Plan approved | Director | Building doesn't start |
| Sensors pass | Automated | Module isn't declared complete |
| Module audited | Review (second session) | Module doesn't go to QA |
| Security verified | Review before production | Nothing goes to production |

**For code review:** open a second Claude Code session dedicated to reviewing. The agent that built does NOT review its own work (self-praise bias).

**For security:** verify before every production deploy:
- API keys in environment variables (never in code)
- User input validated and sanitized
- Queries protected against injection
- Business logic on the server, never on the client
- Error messages without exposing internal details

---

## Git discipline

### Branch per module

```bash
git checkout main && git pull origin main
git checkout -b feature/[module-name]
# work on the branch
# when sensors pass and review is approved:
git checkout main && git merge feature/[module-name]
git push origin main && git branch -d feature/[module-name]
```

Nothing merges to main without Director approval.

### Commit format

```
feat: [module] — [what was built]
fix: [module] — [what was fixed]
refactor: [module] — [what was reorganized]
```

### Why it matters

If a module breaks, revert the branch — not the entire project. Main always works.

---

## Context management

- **`/compact` at 50%** of context. Don't wait for auto-compact. When compacting, state what to preserve.
- **`/clear` when switching modules** completely.
- **Never mix planning and execution** in the same session.
- **If the agent contradicts previous decisions:** context has degraded. Start a new session with CLAUDE.md re-anchored.
- **If context degrades:** it's cheaper to restart than to correct.
- **One task per session.** Focused session > long session.

---

## Session handoff — bridging context windows

The core challenge of long-running agents: each new session starts with no memory of what came before. The handoff protocol solves this.

### At session end (mandatory):
1. Update ESTADO in CLAUDE.md
2. Write/update `progress.md` with structured state (format in BUILDFLOW-PROJETO.md)
3. Git commit with descriptive message
4. If module is incomplete, document exactly where work stopped and what comes next

### At session start (mandatory):
1. Run `bash scripts/init.sh`
2. Read `progress.md`
3. Read git log for recent history
4. Run sensors to check if codebase is healthy
5. If sensors fail, fix existing issues BEFORE starting new work
6. Then begin new work

### Why this matters

Without handoff artifacts, the next agent session guesses at what happened. Guessing wastes tokens and introduces errors. A clean handoff is the difference between an agent that makes progress and an agent that spins in circles.

---

## Agent Teams — when to scale

Use Agent Teams when tasks are genuinely parallel and independent. Examples: frontend + backend + tests simultaneously, research in multiple directions, review of multiple modules.

**DON'T use for:** sequential tasks, edits to the same file, simple tasks where overhead isn't justified.

### How to activate

Requirement: feature flag `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS: 1` in `settings.json`. Requires Opus 4.6.

### How to use

Describe the task and team composition in natural language:

```
Create an agent team with 3 members:
- Frontend: implement components for [module] in [stack]
- Backend: create API endpoints for [module]
- Tests: write integration tests for both
Each one works on their branch. Nobody touches the other's files.
```

### Cost

Agent Teams consume 3-7x more tokens than a single session. Use with intention.

### Rules

- Each teammate receives clear scope and file restrictions
- The Golden Rule applies to all teammates
- The Director can interact directly with any teammate
- Prefer tmux split panes to see all working simultaneously
- Each teammate runs their own sensors before declaring done

---

## Delivery standard

**Approved when:**
- Does exactly what SPEC.md describes
- Follows the structure from ARCH.md
- Matches the Module Plan file by file
- Computational sensors pass (lint + typecheck + tests)
- Passed review in a separate session
- Has no critical security issues

**Rejected when:**
- Does something SPEC.md didn't specify
- Touches files not in the Plan
- Duplicates code that already existed
- Was built without a Module Plan
- Sensors don't pass

The question before every launch: **"If this fails, would I be comfortable explaining why we launched anyway?"** If not — don't launch.

---

## Efficiency radar — weekly review

Once a week, evaluate the project. This is the **steering loop** — how the harness improves over time:

| Detected | Action | Harness component |
|----------|--------|-------------------|
| Same type of module built twice | Create reusable template | Guide (feedforward) |
| Same bug in multiple modules | Add sensor rule or structural test | Sensor (feedback) |
| Agent touching files outside the plan | Reinforce Module Plan discipline | Constraint |
| Agent duplicating existing code | Add "search before creating" rule | Guide (feedforward) |
| Agent ignoring SPEC.md | SPEC.md is too long — split it | Guide (feedforward) |
| Context repeated manually by Director | Add to CLAUDE.md or create Skill | Guide (feedforward) |
| Task executed for the 2nd time | Create Skill or slash command | Guide (feedforward) |
| Sensors catching same issue repeatedly | Add to linter rules or CLAUDE.md | Both |
| Agent self-repair failing consistently | Improve error messages in sensor output | Sensor (feedback) |

The harness is a living system. It improves every week.

---

## Common mistakes

**Coding before architecture.** Everything gets rewritten later. ARCH.md always comes first.

**Skipping the Module Plan.** Agent touches files it shouldn't. One thing breaks another.

**Building everything in one session.** Context fills, agent loses focus. One module per session.

**Not searching for existing code.** Creates component that already exists. Now you have two. Then three.

**Skipping review because "it looks right."** 45% of AI-generated code contains vulnerabilities. "Looks right" is not a quality standard.

**Testing only the happy path.** Works in demo, breaks with real users.

**Deploying without security review.** Business logic on the frontend. Keys in the code.

**Merging directly to main.** Something breaks and affects everything. Branch per module. Main is always clean.

**No init.sh.** Agent starts every session guessing at the state. Wastes tokens, introduces errors.

**No sensors.** Agent declares "done" without verification. Bugs accumulate silently.

**Monolithic CLAUDE.md.** Context is scarce. When every rule is marked "important," none of them are. Keep it under 120 lines.

---

MIT License · Copyright (c) 2026 Caio George Santos
