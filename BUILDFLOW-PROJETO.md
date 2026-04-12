# BUILDFLOW-PROJETO — [Project Name]
# This file is the project's CLAUDE.md. Claude Code reads it automatically every session.
# Version: 4.0 · 2026 · Framework: github.com/caiogeorgesantos/buildflow

---

## Project

- **Name:** [project name]
- **What it is:** [one sentence]
- **Problem it solves:** [one sentence]
- **Who uses it:** [specific audience]
- **Stack:** [languages, frameworks, database, infra]
- **Repository:** [url]
- **Mode:** Solo (default) | Agent Teams (when scaling — see @BUILDFLOW-DEV.md)

---

## Golden Rule

```
REVERSIBLE   → execute + log to ESTADO + report in summary
IRREVERSIBLE → stop + describe the action + wait for Director approval
```

Reversible (act without asking): create files, update ESTADO, reorganize existing content.
Irreversible (stop and ask): delete files, deploy to production, spend money, decisions affecting multiple projects, any action not reversible in 5 minutes.

---

## Mandatory behavior

### Session start
- Run `bash scripts/init.sh` if it exists
- Read `progress.md` if it exists (handoff from previous session)
- If sensors are configured, verify they pass before starting new work

### Before complex tasks
- Interview the Director to understand the complete intent before acting
- For structural tasks, present the proposal FIRST, wait for approval, then execute
- If the request is ambiguous, ASK before assuming

### During execution
- Do ONLY what was requested. No unrequested refactors, no extra features, no library changes without asking, no abstractions for single-use operations
- If you need to deviate, stop and explain why before doing it
- When context passes 50%, alert: "⚠️ Context above 50%. Recommend /compact or new session."

### Before declaring "done"
- Run computational sensors (lint, typecheck, tests) and fix issues found
- If sensors fail after 3 fix attempts, escalate to Director with error details
- List what was done and what remains — never say "done" without evidence

### Session end
- Update ESTADO below
- Write/update `progress.md` (format in @BUILDFLOW-DEV.md)
- Summary: ✅ EXECUTED · ⏳ PENDING · 📝 DECISIONS · ⏭️ NEXT

---

## AI model

- **Sonnet** → Default for 80% of work
- **Haiku** → Research, classification, exploration sub-agents
- **Opus** → Architecture, complex reviews, Agent Teams

Start with Sonnet. Only escalate when genuinely needed.

---

## References

Research/planning: @BUILDFLOW-PESQUISA.md · Development: @BUILDFLOW-DEV.md · Philosophy: @BUILDFLOW.md
Load on demand — don't read all every session.

---

## Project constraints

- [What no agent should do in this project]
- [Files that must not be modified]
- [Mandatory patterns — e.g., "always use TypeScript", "never commit secrets"]

---

## Sensors

```bash
# [Fill with project-specific commands. Examples in @BUILDFLOW-DEV.md]
# lint:      [command]
# typecheck: [command]
# tests:     [command]
```

---

## Business context

[Max 10 lines. Client, objective, audience, revenue model, platforms.
If more is needed, link to a document.]

---

## ESTADO

```
# Updated: [datetime]

## Done
- [specific list with file paths]

## Decisions
- [decision]: [reason] → [impact]

## Pending
- [what remains]

## Next
[one specific action for next session]
```
