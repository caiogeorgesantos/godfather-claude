# 🤵 buildflow
# Document: GLOBAL · Version: 1.0
# Read by: ALL agents, every session

> *"Build like a team of 50. Work like a team of one."*

---

## What is buildflow

A complete framework for building products with AI agents on Claude Code.
Defines how to work — not what to work on.
Each project has its own BUILDFLOW-PROJECT.md that defines what to work on.

---

## Two operating modes — choose before starting

### Mode 1 — Single Agent
One conversation, one agent, direct execution.

**Use when:** solo founder operating without parallel windows, fast iteration needed, one active agent at a time.

**What to use:** SPEC.md, ARCH.md, DECISIONS.md, STATUS.md, MEMORY.md, BUILDFLOW-PROJECT.md. Module Plans only for complex features.

**What to skip:** squad protocol, briefings, handoffs, agent folders, _briefings/ and _templates/.

### Mode 2 — Multi-Agent Squad
Multiple VS Code windows, specialized agents running in parallel.

**Use when:** tasks are genuinely parallel and independent, volume exceeds one context window, multiple modules being built simultaneously.

**What to use:** full framework — all protocols active. Module Plans mandatory. Git branches mandatory per module.

**Note:** Squads use ~15x more tokens than single agent. Only scale when task value justifies it.

**Declare the mode in BUILDFLOW-PROJECT.md before starting any work.**

---

Mandatory reading block for every CLAUDE.md:
```
Before any action, read in this order:
1. ~/Documents/Claude/EN-BUILDFLOW-GLOBAL.md
2. ~/Documents/Claude/EN-BUILDFLOW-ORCHESTRATOR.md  ← Orchestrator only
3. ~/Documents/Claude/EN-BUILDFLOW-AGENT.md          ← Agents only
4. ./BUILDFLOW-PROJECT.md                         ← This project's context
```

---

## Folder structure

```
~/Documents/Claude/
├── EN-BUILDFLOW-GLOBAL.md
├── EN-BUILDFLOW-ORCHESTRATOR.md
├── EN-BUILDFLOW-AGENT.md
├── EN-BUILDFLOW-RESEARCH.md      ← Phase 1
├── EN-BUILDFLOW-DEV.md           ← Phase 7
│
└── your-project/
    ├── CLAUDE.md                → Orchestrator identity
    ├── BUILDFLOW-PROJECT.md     → Agent map and project flow
    ├── SPEC.md                  → What gets built (Phase 3)
    ├── ARCH.md                  → How it gets built (Phase 5)
    ├── MEMORY.md                → Living memory — updated every session
    ├── DECISIONS.md             → Permanent decision log — never deleted
    ├── STATUS.md                → Squad control panel
    ├── _briefings/
    ├── _templates/
    └── agent-name/
        ├── CLAUDE.md
        ├── MEMORY.md
        └── DECISIONS.md
```

---

## Instruction writing rules

- Use bullets, never long paragraphs
- Be specific: "Save in _briefings/" not "save in the right place"
- Put the most important rule first in each section
- Keep every CLAUDE.md under 200 lines
- Over 200 lines → use .claude/rules/ for modular files

---

## The Golden Rule

```
REVERSIBLE   → execute + log in MEMORY.md + report in session summary
IRREVERSIBLE → stop + describe intended action + wait for Director approval
```

**Reversible — act without asking:**
- Create new files
- Update MEMORY.md, DECISIONS.md, STATUS.md
- Generate briefings and handoffs
- Suggest Skills, templates, protocols
- Reorganize content within existing files

**Irreversible — stop and ask:**
- Delete any file or folder
- Modify another agent's CLAUDE.md
- Publish or deploy to production
- Spend money — paid APIs, external services
- Decisions affecting multiple projects
- Any action not reversible within 5 minutes

**End-of-response summary — always when actions were taken:**
```
✅ EXECUTED:
- [action] → [file affected]

⏳ AWAITING APPROVAL:
- [irreversible action] → [reason]
```

---

## When to use squad vs single agent

**Use single agent when:**
- Sequential task with dependencies between steps
- Edits to the same file
- Work requiring shared real-time context
- Simple task with predictable outcome

**Use squad when:**
- Genuinely parallel, independent subtasks
- Research across multiple directions simultaneously
- Volume exceeding one context window
- Distinct modules with no real-time dependency

Note: squads use ~15x more tokens than single agent sessions.
Only scale when the task value justifies it.

---

## Standard files

### MEMORY.md
```
# MEMORY — [agent name]
# Updated: [date time]

## Current session
- Done: [specific list with file paths]
- Decisions: [summary — details in DECISIONS.md]
- Pending: [list]

## Project state
[summary in up to 8 lines]

## Next step
[one specific and clear action]
```

### DECISIONS.md
```
# DECISIONS — [project/agent]

## [date] — [decision title]
- Context: [why it came up]
- Decision: [what was decided]
- Reason: [why this option]
- Impact: [what changes]
```

### STATUS.md — maintained by Orchestrator
```
# STATUS — [project] | Updated: [date]

| Agent  | Last work | Status         | Next step |
|--------|-----------|----------------|-----------|
| [name] | [date]    | ✅ done        | [action]  |
| [name] | [date]    | 🔄 in progress | [action]  |
| [name] | [date]    | ⏸️ paused      | [action]  |
| [name] | [date]    | ⚠️ blocked     | [action]  |
```

---

## File naming standards

```
briefing_[agent]_[YYYYMMDD].md
handoff_[from]_[to]_[YYYYMMDD].md
audit_[agent]_[YYYYMMDD].md
template_[name].md
```

---

## Efficiency Radar

Evaluate at the end of every response. Signal only when genuine.

| Detected situation | Recommended action |
|---|---|
| Task executed for the 2nd time or more | Create a Skill |
| Context manually explained by Director | Add to CLAUDE.md |
| Briefing following a recurring pattern | Create a fixed template |
| Same multi-agent flow repeated | Create a documented protocol |
| Recurring external query | Evaluate MCP or integration |
| Important decision made in conversation | Log in DECISIONS.md now |
| New type of agent mentioned | Create folder and CLAUDE.md |

```
💡 EFFICIENCY RADAR
Detected: [what was identified]
Pattern: [why it seems recurring]
Recommend: [Skill / template / protocol / CLAUDE.md / new agent]
Expected impact: [what it saves]
→ Create now or log as pending?
```

---

## Session closing checklist — mandatory every session

```
□ MEMORY.md updated
□ Important decisions in DECISIONS.md
□ STATUS.md updated (if applicable)
□ Next step documented
□ Execution summary delivered to Director
□ Efficiency Radar evaluated
```

Closing confirmation:
```
📋 SESSION CLOSE
Agent: [name] | Project: [name] | Date: [date]

✅ Done: [list]
📝 Logged: [MEMORY / DECISIONS / STATUS]
⏭️ Next step: [specific action]
⚠️ Awaiting approval: [list or None]
```

---

## Escalation to Director

Escalate when:
- Action is irreversible
- Briefing is ambiguous or incomplete
- Conflict between constitution and project CLAUDE.md
- Expected outcome is unclear
- Something unexpected happened

```
🚨 ESCALATION
Agent: [name]
Situation: [what is blocking]
Options:
  A) [option] → [consequence]
  B) [option] → [consequence]
Recommendation: [suggested option and why]
→ Which path?
```

---

## When to activate the Auditor

- Weekly — routine squad audit
- Before new multi-agent project
- When an agent delivers inconsistent results
- After long sessions with many decisions
- When there's doubt about overlapping responsibilities

---

MIT License · Copyright (c) 2026 Caio George Santos
