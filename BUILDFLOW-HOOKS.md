# BUILDFLOW-HOOKS
# Gates de segurança determinísticos para Claude Code.
# Versão: 3.0 · 2026
# Hooks rodam automaticamente — não dependem da IA lembrar.

> *"Regras que você lembra são sugestões. Regras que rodam automaticamente são regras."*

---

## Hook 1 — Bloqueio de Ação Irreversível ⚠️ OBRIGATÓRIO

Impõe a Regra de Ouro. Bloqueia comandos destrutivos antes de executar.

Adicione ao `.claude/settings.json`:

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"$CLAUDE_TOOL_INPUT\" | grep -qE 'rm -rf|rm -r|git reset --hard|git clean -fd|DROP TABLE|truncate' && echo 'BLOQUEADO: Ação irreversível. Descreva o que quer fazer e aguarde aprovação do Diretor.' >&2 && exit 2 || exit 0"
          }
        ]
      }
    ]
  }
}
```

**Bloqueia:** `rm -rf`, `rm -r`, `git reset --hard`, `git clean -fd`, `DROP TABLE`, `truncate`

**Exit code 2 = bloqueia.** Claude lê a mensagem de erro e para.

---

## Hook 2 — Notificação de Conclusão · RECOMENDADO

Notificação de desktop quando o agente termina. Útil para não ficar olhando o terminal.

```json
{
  "hooks": {
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "osascript -e 'display notification \"Agente terminou — verifique aprovações pendentes\" with title \"buildflow\" sound name \"Glass\"'",
            "async": true
          }
        ]
      }
    ]
  }
}
```

**macOS** (osascript). Para **Linux:** `notify-send "buildflow" "Agente terminou"`.

---

## Instalação

Crie ou edite `.claude/settings.json` na raiz do projeto. Verifique com `/hooks` dentro do Claude Code.

**Regra de segurança:** nunca clique "Sempre permitir" em comandos que contêm tokens/secrets. Use variáveis de ambiente (`${API_TOKEN}`), aí sim é seguro permitir sempre.

Garanta que `.claude/settings.json` está no `.gitignore`.

---

MIT License · Copyright (c) 2026 Caio George Santos
