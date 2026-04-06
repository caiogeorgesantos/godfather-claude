# 🤵 buildflow
# Module: HOOKS
# Version: 1.0 · 2026
# Use: Optional. Recommended for Mode 2 (multi-agent squad).

> *"Rules you remember are suggestions. Rules that run automatically are rules."*

---

## What this module is

BUILDFLOW-HOOKS defines shell commands that execute automatically at specific
points in Claude Code's lifecycle. They transform best-practice guidelines
into technically enforced rules — no agent memory required.

Hooks are configured in `.claude/settings.json` inside each project.

---

## When to use hooks

**Mode 1 — Single Agent:** optional. Useful but not critical.
**Mode 2 — Multi-Agent Squad:** recommended. Multiple agents increase the
risk of one touching something it shouldn't.

---

## The 4 buildflow hooks

### Hook 1 — Irreversible Action Gate (PreToolUse) ⚠️ CRITICAL

Enforces the Golden Rule. Blocks destructive bash commands before they run.
No agent can delete files or reset git without Director approval.

**Add to `.claude/settings.json`:**
```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"$CLAUDE_TOOL_INPUT\" | grep -qE 'rm -rf|rm -r|git reset --hard|git clean -fd|DROP TABLE|truncate' && echo 'BLOCKED: Irreversible action. Requires Director approval. State what you want to do and wait.' >&2 && exit 2 || exit 0"
          }
        ]
      }
    ]
  }
}
```

What it blocks:
- `rm -rf` and `rm -r` — recursive file deletion
- `git reset --hard` — discards all uncommitted changes
- `git clean -fd` — deletes untracked files
- `DROP TABLE` and `truncate` — database destruction

What happens when blocked: Claude Code stops, reads the error message,
and reports to Director instead of proceeding.

---

### Hook 2 — Critical File Protection (PreToolUse)

⚠️ **Read before installing:** This hook blocks ALL edits to DECISIONS.md — including adding new entries. In practice, agents need to append to DECISIONS.md every session. Installing this hook means the agent will be blocked from its own routine work and will need manual intervention every time it tries to log a decision.

**Recommendation: skip Hook 2 for most projects.** The protocol already defines DECISIONS.md as append-only. Trust the rule, not the enforcement. Hook 1 is the one that matters.

**When Hook 2 does make sense:** projects with multiple human contributors where accidental overwrites are a real risk, or high-stakes production systems where an extra gate is worth the friction.

If you install it and want to add a new decision: temporarily disable the hook in settings.json, make the addition, then re-enable.

Prevents agents from editing DECISIONS.md without explicit Director instruction.

**Add to `.claude/settings.json`:**
```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "FILE=$(echo \"$CLAUDE_TOOL_INPUT\" | grep -o '\"path\":\"[^\"]*\"' | cut -d'\"' -f4); echo \"$FILE\" | grep -qE 'DECISIONS\\.md$' && echo 'BLOCKED: DECISIONS.md is a permanent record. Add entries only — never edit or delete existing ones.' >&2 && exit 2 || exit 0"
          }
        ]
      }
    ]
  }
}
```

What it blocks:
- Editing DECISIONS.md (append-only file — agents can add, never modify existing entries)

To allow: Director explicitly instructs the agent to edit DECISIONS.md.

---

### Hook 3 — Completion Notification (Stop)

Fires when Claude Code finishes responding. Sends a desktop notification
so you know the agent is done without staring at the terminal.

**Add to `.claude/settings.json`:**
```json
{
  "hooks": {
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "osascript -e 'display notification \"Agent finished — check for pending approvals\" with title \"buildflow\" sound name \"Glass\"'",
            "async": true
          }
        ]
      }
    ]
  }
}
```

Works on: macOS only (uses osascript).
For Linux: replace with `notify-send "buildflow" "Agent finished"`.
For Windows: replace with `powershell -Command "Add-Type -AssemblyName System.Windows.Forms; [System.Windows.Forms.MessageBox]::Show('Agent finished')"`.

Async: true — runs without blocking Claude Code.

---

### Hook 4 — Session Activity Log (PostToolUse)

Logs every file edited during a session to a daily log file.
Useful for auditing what agents touched across multiple sessions.

**Add to `.claude/settings.json`:**
```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"$(date '+%Y-%m-%d %H:%M:%S') | EDITED | $CLAUDE_TOOL_INPUT_FILE_PATH\" >> ~/Documents/Claude/buildflow-activity.log",
            "async": true
          }
        ]
      }
    ]
  }
}
```

Output: appends to `~/Documents/Claude/buildflow-activity.log`.
Format: `2026-04-05 14:32:11 | EDITED | /path/to/file.md`

Async: true — never slows down the agent.

---

## How to install

### Option A — Project-level (applies only to this project)

Create or edit `.claude/settings.json` in your project root:

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [{ "type": "command", "command": "..." }]
      },
      {
        "matcher": "Edit|Write",
        "hooks": [{ "type": "command", "command": "..." }]
      }
    ],
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [{ "type": "command", "command": "...", "async": true }]
      }
    ],
    "Stop": [
      {
        "hooks": [{ "type": "command", "command": "...", "async": true }]
      }
    ]
  }
}
```

### Option B — Global (applies to all Claude Code projects)

Edit `~/.claude/settings.json` (user home directory).
Hooks 1 and 2 (safety gates) are worth installing globally.
Hooks 3 and 4 (notification and log) work well at project level.

### Verify hooks are active

Inside Claude Code, run:
```
/hooks
```
This shows all configured hooks with their event and matcher.

---

## Complete settings.json with all 4 hooks

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"$CLAUDE_TOOL_INPUT\" | grep -qE 'rm -rf|rm -r|git reset --hard|git clean -fd|DROP TABLE|truncate' && echo 'BLOCKED: Irreversible action. Requires Director approval. State what you want to do and wait.' >&2 && exit 2 || exit 0"
          }
        ]
      },
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "FILE=$(echo \"$CLAUDE_TOOL_INPUT\" | grep -o '\"path\":\"[^\"]*\"' | cut -d'\"' -f4); echo \"$FILE\" | grep -qE 'DECISIONS\\.md$' && echo 'BLOCKED: DECISIONS.md is a permanent record. Add entries only — never edit or delete existing ones.' >&2 && exit 2 || exit 0"
          }
        ]
      }
    ],
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"$(date '+%Y-%m-%d %H:%M:%S') | EDITED | $CLAUDE_TOOL_INPUT_FILE_PATH\" >> ~/Documents/Claude/buildflow-activity.log",
            "async": true
          }
        ]
      }
    ],
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "osascript -e 'display notification \"Agent finished — check for pending approvals\" with title \"buildflow\" sound name \"Glass\"'",
            "async": true
          }
        ]
      }
    ]
  }
}
```

---

## Exit code reference

| Exit code | Effect |
|-----------|--------|
| 0 | Allow — proceed normally |
| 2 | Block — Claude reads stderr and stops |
| 1 | Warning — logs error but proceeds |

Only exit code 2 actually blocks an action.
If a security hook uses exit 1, it provides no enforcement.

---

## Security rule — never hardcode tokens in allowed commands

When Claude Code asks permission to run a command like:
```
curl -H "Authorization: Bearer eyJ0eX..." https://api.example.com
```

**Never click "Always allow"** — this saves the full command including the token to `.claude/settings.json`.

Instead:
1. Click "Allow once" for that specific call
2. Use environment variables for tokens in all future commands:
   ```bash
   curl -H "Authorization: Bearer ${API_TOKEN}" https://api.example.com
   ```
3. Then "Always allow" is safe — the token is not in the command

Check `.claude/settings.json` periodically for hardcoded credentials.
If found: remove the entry, rotate the token if in doubt, and use env vars going forward.

Ensure `.claude/settings.json` is in your `.gitignore`:
```
.claude/settings.json
.claude/settings.local.json
```

---

## Common mistakes

**Mistake 1 — Using exit 1 instead of exit 2 for safety gates**
Exit 1 only warns. Exit 2 enforces. Every blocking hook must use exit 2.

**Mistake 2 — Slow synchronous hooks**
Hooks that take more than 500ms to run make every matched tool call feel
sluggish. Keep hooks fast. Use `"async": true` for logging and notifications.

**Mistake 3 — Hooks too broad**
Matching everything with `"*"` fires on every single tool call.
Be specific with matchers: `"Edit|Write"` not `"*"`.

**Mistake 4 — Installing blocking hooks globally without testing**
Test hooks at project level first. A broken blocking hook can make
Claude Code unusable. Test with `/hooks` and a dry run before going global.

---

MIT License · Copyright (c) 2026 Caio George Santos
