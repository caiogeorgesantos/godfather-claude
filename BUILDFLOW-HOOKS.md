# BUILDFLOW-HOOKS
# Deterministic safety gates and automated sensors for Claude Code.
# Version: 4.0 · 2026
# Hooks run automatically — they don't depend on the AI remembering.

> *"Rules you remember are suggestions. Rules that run automatically are rules."*

---

## Hook architecture

Hooks are the deterministic layer of the harness. They enforce constraints and run sensors without depending on the AI's compliance. Three categories:

| Category | When it runs | What it does | Harness pillar |
|----------|-------------|--------------|----------------|
| **Constraint hooks** | Before tool execution | Block dangerous actions | Constrain |
| **Sensor hooks** | After file changes | Run automated verification | Verify |
| **Lifecycle hooks** | On session stop | Enforce handoff protocol | Correct |

---

## Hook 1 — Irreversible Action Gate ⚠️ MANDATORY

Enforces the Golden Rule. Blocks destructive commands before execution.

Add to `.claude/settings.json`:

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"$CLAUDE_TOOL_INPUT\" | grep -qE 'rm -rf|rm -r|git reset --hard|git clean -fd|DROP TABLE|truncate|git push.*--force' && echo 'BLOCKED: Irreversible action. Describe what you want to do and wait for Director approval.' >&2 && exit 2 || exit 0"
          }
        ]
      }
    ]
  }
}
```

**Blocks:** `rm -rf`, `rm -r`, `git reset --hard`, `git clean -fd`, `git push --force`, `DROP TABLE`, `truncate`

**Exit code 2 = blocked.** Claude reads the error message and stops.

---

## Hook 2 — Completion Notification · RECOMMENDED

Desktop notification when the agent finishes. Useful so you don't have to watch the terminal.

```json
{
  "hooks": {
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "osascript -e 'display notification \"Agent finished — check pending approvals\" with title \"buildflow\" sound name \"Glass\"'",
            "async": true
          }
        ]
      }
    ]
  }
}
```

**macOS** (osascript). For **Linux:** `notify-send "buildflow" "Agent finished"`.

---

## Hook 3 — Computational Sensors · RECOMMENDED

Runs linter, typecheck, and tests automatically after file modifications. This is the feedback loop that enables self-repair.

**For Next.js / TypeScript projects:**

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit|MultiEdit",
        "hooks": [
          {
            "type": "command",
            "command": "cd \"$(git rev-parse --show-toplevel 2>/dev/null || pwd)\" && FILE=$(echo \"$CLAUDE_TOOL_INPUT\" | grep -oP '\"file_path\":\\s*\"\\K[^\"]+' || echo \"$CLAUDE_TOOL_INPUT\" | grep -oP '\"path\":\\s*\"\\K[^\"]+') && if echo \"$FILE\" | grep -qE '\\.(ts|tsx|js|jsx)$'; then npx biome check \"$FILE\" --no-errors-on-unmatched 2>&1 | tail -5; fi",
            "timeout": 15000
          }
        ]
      }
    ]
  }
}
```

**For Python projects:**

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit|MultiEdit",
        "hooks": [
          {
            "type": "command",
            "command": "cd \"$(git rev-parse --show-toplevel 2>/dev/null || pwd)\" && FILE=$(echo \"$CLAUDE_TOOL_INPUT\" | grep -oP '\"file_path\":\\s*\"\\K[^\"]+' || echo \"$CLAUDE_TOOL_INPUT\" | grep -oP '\"path\":\\s*\"\\K[^\"]+') && if echo \"$FILE\" | grep -qE '\\.py$'; then ruff check \"$FILE\" 2>&1 | tail -5; fi",
            "timeout": 15000
          }
        ]
      }
    ]
  }
}
```

**How it works:** After every file write/edit, the hook runs the linter on the changed file. If there are errors, the output is shown to Claude, who reads them and self-corrects. This happens in real-time, not at the end.

**Timeout:** 15 seconds. If the sensor takes longer (large projects), increase or simplify the check.

**Self-repair behavior:** Claude sees the linter output as part of the tool result. If there are errors, Claude should fix them immediately before continuing. If the same error persists after 3 edits, Claude should stop and report to the Director.

---

## Hook 4 — Pre-Commit Verification · OPTIONAL

Runs full sensor suite before any git commit. Prevents committing broken code.

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "if echo \"$CLAUDE_TOOL_INPUT\" | grep -qE 'git commit'; then cd \"$(git rev-parse --show-toplevel 2>/dev/null || pwd)\" && echo '🔍 Running pre-commit sensors...' && npx biome check src/ --no-errors-on-unmatched 2>&1 | tail -3 && npx tsc --noEmit 2>&1 | tail -3 && npm test -- --silent 2>&1 | tail -5 && echo '✅ All sensors passed' || (echo '❌ BLOCKED: Sensors failed. Fix issues before committing.' >&2 && exit 2); fi",
            "timeout": 60000
          }
        ]
      }
    ]
  }
}
```

**What it does:** Intercepts `git commit` and runs the full lint + typecheck + test suite first. If any fail, the commit is blocked (exit 2).

**Timeout:** 60 seconds. Adjust for test suite size.

---

## Combining hooks

All hooks can be combined in a single `.claude/settings.json`. Here's the recommended full setup:

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"$CLAUDE_TOOL_INPUT\" | grep -qE 'rm -rf|rm -r|git reset --hard|git clean -fd|DROP TABLE|truncate|git push.*--force' && echo 'BLOCKED: Irreversible action. Describe what you want to do and wait for Director approval.' >&2 && exit 2 || exit 0"
          }
        ]
      },
      {
        "matcher": "Write|Edit|MultiEdit",
        "hooks": [
          {
            "type": "command",
            "command": "FILE=$(echo \"$CLAUDE_TOOL_INPUT\" | grep -oP '\"file_path\":\\s*\"\\K[^\"]+' || echo \"$CLAUDE_TOOL_INPUT\" | grep -oP '\"path\":\\s*\"\\K[^\"]+') && ROOT=$(git rev-parse --show-toplevel 2>/dev/null || pwd) && ALLOWED=\"$ROOT/.claude/allowed-paths.txt\" && if [ -f \"$ALLOWED\" ]; then MATCH=0; while IFS= read -r pattern || [ -n \"$pattern\" ]; do pattern=$(echo \"$pattern\" | sed 's/^[[:space:]]*//;s/[[:space:]]*$//'); [ -z \"$pattern\" ] && continue; echo \"$FILE\" | grep -q \"^$pattern\" && MATCH=1 && break; done < \"$ALLOWED\"; [ $MATCH -eq 0 ] && echo \"BLOCKED: File $FILE is outside allowed paths. Check .claude/allowed-paths.txt or update the Module Plan.\" >&2 && exit 2; fi",
            "timeout": 5000
          }
        ]
      }
    ],
    "PostToolUse": [
      {
        "matcher": "Write|Edit|MultiEdit",
        "hooks": [
          {
            "type": "command",
            "command": "cd \"$(git rev-parse --show-toplevel 2>/dev/null || pwd)\" && FILE=$(echo \"$CLAUDE_TOOL_INPUT\" | grep -oP '\"file_path\":\\s*\"\\K[^\"]+' || echo \"$CLAUDE_TOOL_INPUT\" | grep -oP '\"path\":\\s*\"\\K[^\"]+') && if echo \"$FILE\" | grep -qE '\\.(ts|tsx|js|jsx)$'; then npx biome check \"$FILE\" --no-errors-on-unmatched 2>&1 | tail -5; fi",
            "timeout": 15000
          }
        ]
      }
    ],
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "osascript -e 'display notification \"Agent finished — check pending approvals\" with title \"buildflow\" sound name \"Glass\"'",
            "async": true
          }
        ]
      }
    ]
  }
}
```

---

## Installation

Create or edit `.claude/settings.json` at the project root. Verify with `/hooks` inside Claude Code.

**Security rules:**
- Never click "Always allow" on commands that contain tokens/secrets. Use environment variables (`${API_TOKEN}`), then it's safe to always allow.
- Make sure `.claude/settings.json` is in `.gitignore`.
- Hook commands should never contain credentials or API keys.

---

## Hook 5 — Filesystem Sandbox · RECOMMENDED

Restricts which directories the agent can modify. Enforces the Module Plan deterministically — the agent can't write outside allowed paths even if it "forgets" the plan.

Create a file `.claude/allowed-paths.txt` at the project root listing the directories the agent can touch:

```
src/
tests/
scripts/
progress.md
```

Then add this hook:

```json
{
  "matcher": "Write|Edit|MultiEdit",
  "hooks": [
    {
      "type": "command",
      "command": "FILE=$(echo \"$CLAUDE_TOOL_INPUT\" | grep -oP '\"file_path\":\\s*\"\\K[^\"]+' || echo \"$CLAUDE_TOOL_INPUT\" | grep -oP '\"path\":\\s*\"\\K[^\"]+') && ROOT=$(git rev-parse --show-toplevel 2>/dev/null || pwd) && ALLOWED=\"$ROOT/.claude/allowed-paths.txt\" && if [ -f \"$ALLOWED\" ]; then MATCH=0; while IFS= read -r pattern || [ -n \"$pattern\" ]; do pattern=$(echo \"$pattern\" | sed 's/^[[:space:]]*//;s/[[:space:]]*$//'); [ -z \"$pattern\" ] && continue; echo \"$FILE\" | grep -q \"^$pattern\" && MATCH=1 && break; done < \"$ALLOWED\"; [ $MATCH -eq 0 ] && echo \"BLOCKED: File $FILE is outside allowed paths. Check .claude/allowed-paths.txt or update the Module Plan.\" >&2 && exit 2; fi",
      "timeout": 5000
    }
  ]
}
```

**How it works:** Before every file write/edit, the hook checks if the target path starts with any pattern listed in `.claude/allowed-paths.txt`. If the file doesn't exist, the hook is a no-op (sandbox is optional per project). If the file exists and the path doesn't match, the write is blocked.

**When to use:** Update `.claude/allowed-paths.txt` at the start of each module to match the Module Plan's file list. This turns the Module Plan from a suggestion into an enforced boundary.

**Limitation:** This catches Write/Edit/MultiEdit tool calls but not file writes via Bash (e.g., `echo > file.txt`). Hook 1 already blocks the most dangerous Bash operations; for full sandboxing, combine both hooks.

---

## Writing custom sensors

The harness improves through the steering loop: when an issue recurs, add a sensor for it.

**Good sensor design:**
- Output is concise (use `tail -N` to limit)
- Error messages are actionable (tell the agent *what* to fix, not just *that* something is wrong)
- Timeout is set appropriately
- False positives are minimized (they train the agent to ignore sensor output)

**Custom sensor example — check for hardcoded secrets:**

```json
{
  "matcher": "Write|Edit|MultiEdit",
  "hooks": [
    {
      "type": "command",
      "command": "FILE=$(echo \"$CLAUDE_TOOL_INPUT\" | grep -oP '\"file_path\":\\s*\"\\K[^\"]+' || echo \"$CLAUDE_TOOL_INPUT\" | grep -oP '\"path\":\\s*\"\\K[^\"]+') && if grep -qE '(sk-[a-zA-Z0-9]{20,}|AKIA[A-Z0-9]{16}|ghp_[a-zA-Z0-9]{36})' \"$FILE\" 2>/dev/null; then echo 'SENSOR: Possible hardcoded secret detected. Move to environment variable.' >&2 && exit 2; fi",
      "timeout": 5000
    }
  ]
}
```

---

## Hook reference

| Hook | Category | Pillar | When | What |
|------|----------|--------|------|------|
| Hook 1 | Constraint | Constrain | PreToolUse (Bash) | Blocks irreversible commands |
| Hook 2 | Lifecycle | Correct | Stop | Notifies Director |
| Hook 3 | Sensor | Verify | PostToolUse (Write/Edit) | Runs linter on changed files |
| Hook 4 | Sensor | Verify | PreToolUse (git commit) | Full sensor suite before commit |
| Hook 5 | Constraint | Constrain | PreToolUse (Write/Edit) | Blocks writes outside allowed paths |

---

MIT License · Copyright (c) 2026 Caio George Santos
