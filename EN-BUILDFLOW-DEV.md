# 🤵 buildflow
# Module: DEV
# Version: 2.0 · 2026
# Use: After SPEC.md and ARCH.md are approved. Before Claude Code opens.

> *"A well-made foundation prevents exponential rework."*

---

## What this module is

BUILDFLOW-DEV is the protocol for building products with Claude Code.
It starts only after SPEC.md and ARCH.md exist and are approved.
It ends only when the product passes quality criteria.
It applies to any product type: landing pages, systems, apps, portals.

---

## Non-negotiable entry criteria

Before opening Claude Code, confirm:

- [ ] SPEC.md exists and has been approved by Director
- [ ] ARCH.md exists and has been approved by Director
- [ ] Stack has been defined
- [ ] All open questions in SPEC.md have been resolved
- [ ] buildflow framework files are in ~/Documents/Claude/
- [ ] Git repository has been created with main branch
- [ ] BUILDFLOW-PROJECT.md has been created for this project

**If any of these is missing: do not open Claude Code.**

---

## The Development Squad — Claude Code

Each agent runs in a separate VS Code window.
Each window points to the project folder.
Each agent has its own CLAUDE.md, MEMORY.md, and DECISIONS.md.

### Standard Development Squad

| Agent | Role | When to activate |
|-------|------|-----------------|
| Orchestrator | Coordinates squad, maintains STATUS.md | Always active |
| Architect | Defines ARCH.md + module plans before each module | Phase 0 + before each module |
| Developer | Writes the code using specialized writers | Phase 1+ |
| Code Auditor | Reviews every delivery from Developer | After every delivery |
| QA Tester | Tests what was built | After Auditor approves |
| Security Reviewer | Checks for vulnerabilities | Before production |

### Rules for the development squad

- No agent writes code before the Architect delivers ARCH.md
- No agent writes code before the Architect delivers the module plan
- No feature goes to QA before passing Code Auditor
- No code goes to production before Security Reviewer approves
- Every agent reads SPEC.md and ARCH.md before starting
- Every agent follows EN-BUILDFLOW-GLOBAL.md rules

---

## Development Phases

### Phase 0 — Architecture (Architect agent)

The Architect reads SPEC.md and delivers ARCH.md:

```
ARCH.md containing:
- Folder and file structure
- Database schema (tables, fields, relationships)
- API contracts (endpoints, inputs, outputs)
- Component map (what connects to what)
- Environment variables needed
- Third-party integrations and how they connect
- Module list in execution order with dependencies
```

Rules:
- No code is written in this phase — only structure
- Director approves ARCH.md before Phase 1 starts
- If ARCH.md changes during development, all agents are notified

Briefing for Architect:
```
Read SPEC.md and EN-BUILDFLOW-GLOBAL.md.
Your mission: define the complete architecture for this product.
Do NOT write code. Define structure only.
Every decision must be justified by SPEC.md requirements.
Deliver ARCH.md. Await Director approval before anything is built.
```

---

### Phase 1 — Module Planning (Architect agent, before each module)

Before the Developer touches any module, the Architect runs /plan.

The /plan phase does two things:
1. Searches INSIDE the project for existing code to reuse
2. Searches OUTSIDE the project for documented patterns and best practices

The Architect delivers a Module Plan containing:

```
MODULE PLAN — [module name]
Branch: feature/[module-name]

Overview: [what this module does in one sentence]

Files to CREATE:
- [exact path] — [what it contains]
- [exact path] — [what it contains]

Files to MODIFY:
- [exact path] — [what changes and why]

Files to REUSE (already exist):
- [exact path] — [how it will be used]

Behaviors:
- Happy path: [what happens when everything works]
- Edge cases: [what happens at the limits]
- Error states: [what happens when it fails]

Database changes (if any):
- [table] — [what changes]

External dependencies (if any):
- [service/API] — [how it's used]

Writer agents needed:
- [writer type] — [which files]
```

Rules:
- Director approves Module Plan before Developer starts
- If a file is not in the plan, Developer does not touch it
- This is the single most important rule to prevent "AI disobedience"

---

### Phase 2 — Construction (Developer agent)

The Developer builds one module at a time using the Module Plan.
Never builds beyond what the plan specifies.

#### Specialized Writer Agents

The Developer uses specialized writers by file type.
Each writer has its own rules and patterns:

| Writer | Responsibility |
|--------|---------------|
| component-writer | Visual elements — buttons, forms, cards, layouts |
| action-writer | Server-side logic — processes user actions, saves data |
| hook-writer | Connects UI to server actions — the "wire" between them |
| integration-writer | External services — email, payments, APIs |
| model-writer | Database structure — tables, schemas, relationships |
| route-writer | API endpoints — communication between frontend and backend |
| test-writer | Automated tests — unit, integration, e2e |

Rules for each writer:
- Only touches files listed in the Module Plan
- Searches for existing components before creating new ones
- Never duplicates code that already exists in the project
- Always follows the patterns in ARCH.md — never invents new ones

Briefing for Developer:
```
Read SPEC.md, ARCH.md, the Module Plan, and EN-BUILDFLOW-GLOBAL.md.
Your mission: build [module name] exactly as specified in the Module Plan.
Use the appropriate writer agent for each file type.
Only touch files listed in the Module Plan.
Before creating anything: search the project for existing code to reuse.
Follow ARCH.md patterns exactly. If you need to deviate, stop and flag it.
After completing: deliver a summary of what was built for the Code Auditor.
```

---

### Phase 3 — Audit (Code Auditor agent)

The Code Auditor reviews every module the Developer delivers.
This is not optional. Every delivery goes through audit.

What the Auditor checks:
- Does the code do what SPEC.md requires
- Does it follow ARCH.md structure
- Does it match the Module Plan exactly — no extra files, no missing files
- Is there duplicate code that already existed in the project
- Are there obvious bugs or edge cases not handled
- Are there hardcoded values that should be environment variables
- Is error handling present and meaningful
- Is the code readable by a future agent

Audit report format:
```
# CODE AUDIT — [module name]
# Date: [date]

## VERDICT: APPROVED / NEEDS REVISION

## Files checked vs Module Plan
- [file] — in plan: yes/no — created/modified: yes/no

## Issues found
### Critical (must fix before QA):
- [issue + location + suggested fix]

### Important (fix before production):
- [issue + location + suggested fix]

### Minor (nice to have):
- [issue + location + suggested fix]

## What the Developer did well
[at least one positive — prevents over-correction]
```

Briefing for Code Auditor:
```
Read SPEC.md, ARCH.md, the Module Plan, and EN-BUILDFLOW-GLOBAL.md.
Your mission: audit [module name] delivered by the Developer.
Cross-reference every file against the Module Plan.
Flag any file touched that was not in the plan.
Flag any duplicate code found in the project.
Your verdict (APPROVED / NEEDS REVISION) gates QA.
Nothing moves to QA without your approval.
```

---

### Phase 4 — Testing (QA Tester agent)

The QA Tester tests what the Auditor approved.

What the Tester checks:
- Does it work as described in SPEC.md (happy path)
- What happens at the edges (empty fields, max length, invalid input)
- What happens when integrations fail (API down, database timeout)
- Does it work on mobile (if applicable)
- Does it work on different browsers (if applicable)
- Are error messages clear and helpful to the user

Test report format:
```
# QA REPORT — [module name]
# Date: [date]

## VERDICT: PASSED / FAILED

## Tests run
| Test | Expected | Result | Status |
|------|----------|--------|--------|
| [test] | [expected] | [actual] | ✅/❌ |

## Bugs found
### Blockers (must fix before merge):
- [bug + steps to reproduce + expected behavior]

### Non-blockers (fix before production):
- [bug + steps to reproduce + expected behavior]
```

Briefing for QA Tester:
```
Read SPEC.md and EN-BUILDFLOW-GLOBAL.md.
Your mission: test [module name] that passed Code Audit.
Test the happy path first. Then break it.
Every bug needs: what you did, what happened, what should have happened.
Your verdict (PASSED / FAILED) gates merge to main.
```

---

### Phase 5 — Security Review (Security agent)

Runs once — before the product goes to production.
Not after every module — only at the end.

What the Security Reviewer checks:
- Are API keys and secrets in environment variables (never in code)
- Is user input validated and sanitized
- Are database queries protected against injection
- Is authentication implemented correctly
- Are sensitive routes protected
- Is business logic on the server, never on the client
- Are error messages safe (not exposing internal details)
- Are dependencies up to date and without known vulnerabilities

Security report format:
```
# SECURITY REPORT
# Date: [date]
# Status: CLEARED FOR PRODUCTION / BLOCKED

## Critical issues (block production):
- [issue + risk + fix]

## Important issues (fix within 30 days):
- [issue + risk + fix]

## Recommendations:
- [best practice not yet implemented]
```

---

## Git Discipline

### Branch per module — not per day, not per session

Every module gets its own branch before the Developer writes a single line.

```bash
git checkout main
git pull origin main
git checkout -b feature/[module-name]
```

Work happens on the branch. When QA passes:

```bash
git checkout main
git merge feature/[module-name]
git push origin main
git branch -d feature/[module-name]
```

Director approves merge. Orchestrator executes it.
Nothing merges to main without QA approval.

### Commit format — inside the branch

```
feat: [module name] — [one line of what was built]
fix: [module name] — [one line of what was fixed]
```

### Why branches matter

If a module breaks, you revert the branch — not the entire project.
Main always contains working, approved code.
You can show the product at any point without fear.

---

## Context Management

Claude Code loses focus when context fills up.
Symptoms: contradicting earlier decisions, inconsistent patterns,
ignoring CLAUDE.md instructions, touching files not in the plan.

Rules:
- Run /compact when context reaches 50%
- Run /clear when switching to a completely different module
- Never mix planning and execution in the same session
- If the agent starts contradicting ARCH.md: start a fresh session
  with SPEC.md, ARCH.md, Module Plan, and CLAUDE.md re-anchored
- If context degrades: it's cheaper to restart than to fix the mess

---

## Quality Gates — Nothing Passes Without These

| Gate | Who approves | What blocks if not passed |
|------|-------------|--------------------------|
| SPEC.md approved | Director | Nothing gets built |
| ARCH.md approved | Director | No code gets written |
| Module Plan approved | Director | Developer doesn't start |
| Module audited | Code Auditor | Module doesn't go to QA |
| Module tested | QA Tester | Module doesn't merge to main |
| Security cleared | Security Reviewer | Nothing goes to production |

---

## The Standard That Applies to Every Project

A delivery is approved when:
- It does exactly what SPEC.md describes
- It follows ARCH.md structure
- It matches the Module Plan file by file
- It passes Code Audit
- It passes QA
- It has no critical security issues

A delivery is rejected when:
- It does something SPEC.md didn't specify
- It contradicts ARCH.md
- It touches files not in the Module Plan
- It duplicates code that already existed
- It has critical bugs
- It was built without a Module Plan

The question before every release:
**"If this fails, would I be comfortable explaining why we shipped it anyway?"**
If the answer is no — do not ship.

---

## Efficiency Radar — Dev Edition

At the end of every session, check:

| Detected | Action |
|----------|--------|
| Same type of module built twice | Create a reusable template |
| Same bug found in multiple modules | Add rule to Code Auditor briefing |
| Same QA test repeated across modules | Create a test checklist |
| Same ARCH.md question asked twice | Update ARCH.md with the answer |
| Agent touching files not in the plan | Reinforce Module Plan discipline |
| Agent duplicating existing code | Add search-first rule to Developer briefing |
| Agent ignoring SPEC.md | SPEC.md is too long — split by module |

---

## Session Closing — Dev Edition

Before closing any development session:

```
□ Current module: APPROVED by Auditor / PASSED QA / or clearly marked as IN PROGRESS
□ Branch committed (if module is complete — merge to main after QA)
□ MEMORY.md updated with what was built
□ DECISIONS.md updated with any architectural decisions made
□ STATUS.md updated
□ Next module clearly defined in MEMORY.md
□ Any open questions escalated to Director
```

---

## Common Mistakes — Learn From Real Projects

**Mistake 1 — Starting to code before architecture is defined**
The Developer builds something, the Architect arrives and says
the structure is wrong. Everything gets rewritten.
Fix: Architect always goes first. ARCH.md before any code.

**Mistake 2 — Skipping the Module Plan**
The Developer touches files that weren't supposed to change.
One thing breaks another. The "poor man's blanket" problem.
Fix: Module Plan is mandatory. Every module. No exceptions.

**Mistake 3 — Building the entire product in one session**
Context fills, the agent loses focus, inconsistencies appear.
Fix: One module per session. Branch. Audit. Test. Merge.

**Mistake 4 — Not searching for existing code before writing**
The Developer creates a button component that already exists.
Now there are two. Then three. Maintenance becomes impossible.
Fix: search-first is part of every Developer briefing.

**Mistake 5 — Skipping Code Audit because "it looks fine"**
45% of AI-generated code contains vulnerabilities.
"Looks fine" is not a quality standard.
Fix: Code Audit is mandatory. No exceptions.

**Mistake 6 — Testing only the happy path**
The product works perfectly in demos and breaks with real users.
Fix: QA Tester explicitly tests edge cases and failure scenarios.

**Mistake 7 — Going to production without security review**
Business logic on the frontend. API keys in the code.
Any person with browser dev tools can exploit this.
Fix: Security Reviewer runs once before every production deployment.

**Mistake 8 — Merging directly to main without branch**
Something breaks and affects everything that was working.
Fix: Branch per module. Main is always clean and working.

---

MIT License · Copyright (c) 2026 Caio George Santos
