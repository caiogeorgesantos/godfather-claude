# BUILDFLOW-PROJECT — [Project Name]
# Version: 1.0 | Created: [date] | Maintained by: Orchestrator

---

## Project description

[One sentence describing the project and its main objective]

---

## Operating mode



---

## Operating mode

Declare before starting any work:

```
Operating mode: [ ] Mode 1 — Single Agent / [ ] Mode 2 — Multi-Agent Squad

Mode 1: one conversation, one agent. Use control files only.
Skip: squad protocol, briefings, handoffs, agent folders.
Module Plans: only for complex features.

Mode 2: multiple VS Code windows, agents in parallel.
Use: full framework, all protocols active.
Module Plans and Git branches: mandatory per module.
```

---

## Project type

```
Project type: [ ] New (starting from scratch) / [ ] Existing (already has documentation)

If NEW:
- SPEC.md: full document — created in Phase 3
- ARCH.md: full document — created in Phase 5

If EXISTING:
- SPEC.md: lightweight wrapper (~100 lines) — index + gate pointing to existing docs
- ARCH.md: lightweight wrapper (~100 lines) — index + gate pointing to existing technical docs
- Existing documentation: [list key documents and their locations]
```

---

## Key documents

| Document | Status | Location | Owner |
|----------|--------|----------|-------|
| SPEC.md | [ ] pending / [x] approved | ./SPEC.md | Director |
| ARCH.md | [ ] pending / [x] approved | ./ARCH.md | Architect |
| BUILDFLOW-PROJECT.md | [x] active | ./BUILDFLOW-PROJECT.md | Orchestrator |
| MEMORY.md | [x] active | ./MEMORY.md | Orchestrator |
| DECISIONS.md | [x] active | ./DECISIONS.md | All agents |
| STATUS.md | [x] active | ./STATUS.md | Orchestrator |

**SPEC.md not approved → nothing gets specified or built.**
**ARCH.md not approved → no code gets written.**

---

## Squad map

| Agent | Folder | Role | Receives from | Delivers to |
|-------|--------|------|---------------|-------------|
| Orchestrator | ./ | Coordinates the squad | Director | All agents |
| [Agent 1] | ./[folder] | [role] | [source] | [destination] |
| [Agent 2] | ./[folder] | [role] | [source] | [destination] |
| Auditor | ./auditor | Audits agents and deliverables | Orchestrator | Director |

---

## Standard workflow

```
Director → briefing → Orchestrator
Orchestrator → maps agents → generates briefings → awaits approval
Director → approves → Orchestrator releases
Agent 1 → executes → handoff → Agent 2
Agent 2 → executes → delivers → Orchestrator
Orchestrator → consolidates → delivers → Director
```

---

## When NOT to use a squad in this project

- [List task types that a single agent handles better]
- Example: one-off edits to a single file
- Example: tasks with less than 2h estimated work

---

## Standard deliverables

| Deliverable | Format | Save in | Owner |
|-------------|--------|---------|-------|
| [name] | [.md / .html / etc] | [path] | [agent] |

---

## Project restrictions

- [What no agent should do in this project]
- [Files that must not be modified]
- [Mandatory patterns]

---

## Business context

[Information all agents need about this project:
client, goal, audience, platforms involved, etc.]

---

## BUILDFLOW-PROJECT version history

| Date | Change |
|------|--------|
| [date] | Initial creation |

---

## License

MIT License — Copyright (c) 2026 Caio George Santos
