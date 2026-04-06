# 🤵 buildflow
# Módulo: HOOKS
# Versão: 1.0 · 2026
# Uso: Opcional. Recomendado para Modo 2 (squad multi-agente).

> *"Regras que você lembra são sugestões. Regras que rodam automaticamente são regras."*

---

## O que é este módulo

BUILDFLOW-HOOKS define comandos shell que executam automaticamente em pontos
específicos do ciclo de vida do Claude Code. Eles transformam as boas práticas
do framework em regras tecnicamente impostas — sem depender da memória do agente.

Hooks são configurados em `.claude/settings.json` dentro de cada projeto.

---

## Quando usar hooks

**Modo 1 — Agente Único:** opcional. Útil mas não crítico.
**Modo 2 — Squad Multi-Agente:** recomendado. Múltiplos agentes aumentam o
risco de um tocar em algo que não deveria.

---

## Os 4 hooks do buildflow

### Hook 1 — Bloqueio de Ação Irreversível (PreToolUse) ⚠️ CRÍTICO

Impõe a Regra de Ouro. Bloqueia comandos bash destrutivos antes de executarem.
Nenhum agente pode deletar arquivos ou resetar o git sem aprovação do Diretor.

**Adicione ao `.claude/settings.json`:**
```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"$CLAUDE_TOOL_INPUT\" | grep -qE 'rm -rf|rm -r|git reset --hard|git clean -fd|DROP TABLE|truncate' && echo 'BLOQUEADO: Ação irreversível. Requer aprovação do Diretor. Descreva o que quer fazer e aguarde.' >&2 && exit 2 || exit 0"
          }
        ]
      }
    ]
  }
}
```

O que bloqueia:
- `rm -rf` e `rm -r` — deleção recursiva de arquivos
- `git reset --hard` — descarta todas as mudanças não commitadas
- `git clean -fd` — deleta arquivos não rastreados
- `DROP TABLE` e `truncate` — destruição de banco de dados

O que acontece quando bloqueado: o Claude Code para, lê a mensagem de erro,
e reporta ao Diretor em vez de prosseguir.

---

### Hook 2 — Proteção de Arquivos Críticos (PreToolUse)

⚠️ **Leia antes de instalar:** Este hook bloqueia TODAS as edições no DECISIONS.md — inclusive adicionar novas entradas. Na prática, os agentes precisam fazer append no DECISIONS.md toda sessão. Instalar este hook significa que o agente ficará bloqueado em seu trabalho rotineiro e precisará de intervenção manual toda vez que tentar registrar uma decisão.

**Recomendação: não instale o Hook 2 na maioria dos projetos.** O protocolo já define o DECISIONS.md como append-only. Confie na regra, não na imposição técnica. O Hook 1 é o que realmente importa.

**Quando o Hook 2 faz sentido:** projetos com múltiplos contribuidores humanos onde sobrescritas acidentais são um risco real, ou sistemas de produção de alto risco onde a fricção extra vale a pena.

Se instalar e precisar adicionar uma nova decisão: desative o hook temporariamente no settings.json, faça a adição, depois reative.

Impede que agentes editem o DECISIONS.md sem instrução explícita do Diretor.

**Adicione ao `.claude/settings.json`:**
```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "FILE=$(echo \"$CLAUDE_TOOL_INPUT\" | grep -o '\"path\":\"[^\"]*\"' | cut -d'\"' -f4); echo \"$FILE\" | grep -qE 'DECISIONS\\.md$' && echo 'BLOQUEADO: DECISIONS.md é um registro permanente. Apenas adicione entradas — nunca edite ou delete as existentes.' >&2 && exit 2 || exit 0"
          }
        ]
      }
    ]
  }
}
```

O que bloqueia:
- Edição do DECISIONS.md (arquivo append-only — agentes podem adicionar, nunca modificar entradas existentes)

Para permitir: Diretor instrui explicitamente o agente a editar o DECISIONS.md.

---

### Hook 3 — Notificação de Conclusão (Stop)

Dispara quando o Claude Code termina de responder. Envia uma notificação
de desktop para você saber que o agente terminou sem ficar olhando para o terminal.

**Adicione ao `.claude/settings.json`:**
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

Funciona em: macOS apenas (usa osascript).
Para Linux: substitua por `notify-send "buildflow" "Agente terminou"`.

Async: true — roda sem bloquear o Claude Code.

---

### Hook 4 — Log de Atividade da Sessão (PostToolUse)

Registra cada arquivo editado durante uma sessão em um arquivo de log diário.
Útil para auditar o que os agentes tocaram em múltiplas sessões.

**Adicione ao `.claude/settings.json`:**
```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"$(date '+%Y-%m-%d %H:%M:%S') | EDITADO | $CLAUDE_TOOL_INPUT_FILE_PATH\" >> ~/Documents/Claude/buildflow-activity.log",
            "async": true
          }
        ]
      }
    ]
  }
}
```

Output: adiciona ao `~/Documents/Claude/buildflow-activity.log`.
Formato: `2026-04-05 14:32:11 | EDITADO | /caminho/para/arquivo.md`

Async: true — nunca atrasa o agente.

---

## Como instalar

### Opção A — Nível de projeto (aplica apenas a este projeto)

Crie ou edite `.claude/settings.json` na raiz do seu projeto.

### Opção B — Global (aplica a todos os projetos Claude Code)

Edite `~/.claude/settings.json` (diretório home do usuário).
Os Hooks 1 e 2 (bloqueios de segurança) valem a pena instalar globalmente.
Os Hooks 3 e 4 (notificação e log) funcionam bem no nível de projeto.

### Verificar se os hooks estão ativos

Dentro do Claude Code, execute:
```
/hooks
```
Isso mostra todos os hooks configurados com seu evento e matcher.

---

## settings.json completo com os 4 hooks

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"$CLAUDE_TOOL_INPUT\" | grep -qE 'rm -rf|rm -r|git reset --hard|git clean -fd|DROP TABLE|truncate' && echo 'BLOQUEADO: Ação irreversível. Requer aprovação do Diretor. Descreva o que quer fazer e aguarde.' >&2 && exit 2 || exit 0"
          }
        ]
      },
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "FILE=$(echo \"$CLAUDE_TOOL_INPUT\" | grep -o '\"path\":\"[^\"]*\"' | cut -d'\"' -f4); echo \"$FILE\" | grep -qE 'DECISIONS\\.md$' && echo 'BLOQUEADO: DECISIONS.md é um registro permanente. Apenas adicione entradas — nunca edite ou delete as existentes.' >&2 && exit 2 || exit 0"
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
            "command": "echo \"$(date '+%Y-%m-%d %H:%M:%S') | EDITADO | $CLAUDE_TOOL_INPUT_FILE_PATH\" >> ~/Documents/Claude/buildflow-activity.log",
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
            "command": "osascript -e 'display notification \"Agente terminou — verifique aprovações pendentes\" with title \"buildflow\" sound name \"Glass\"'",
            "async": true
          }
        ]
      }
    ]
  }
}
```

---

## Referência de exit codes

| Exit code | Efeito |
|-----------|--------|
| 0 | Permite — prossegue normalmente |
| 2 | Bloqueia — Claude lê o stderr e para |
| 1 | Aviso — registra o erro mas prossegue |

Apenas o exit code 2 realmente bloqueia uma ação.
Se um hook de segurança usar exit 1, não há imposição real.

---

## Regra de segurança — nunca hardcode tokens em comandos permitidos

Quando o Claude Code pede permissão para rodar um comando como:
```
curl -H "Authorization: Bearer eyJ0eX..." https://api.example.com
```

**Nunca clique em "Sempre permitir"** — isso salva o comando completo incluindo o token no `.claude/settings.json`.

Em vez disso:
1. Clique em "Permitir uma vez" para aquela chamada específica
2. Use variáveis de ambiente para tokens em todos os comandos futuros:
   ```bash
   curl -H "Authorization: Bearer ${API_TOKEN}" https://api.example.com
   ```
3. Aí "Sempre permitir" é seguro — o token não está no comando

Verifique periodicamente o `.claude/settings.json` para credenciais hardcoded.
Se encontrar: remova a entrada, rode novos tokens se necessário, e use variáveis de ambiente.

Garanta que `.claude/settings.json` está no seu `.gitignore`:
```
.claude/settings.json
.claude/settings.local.json
```

---

## Erros comuns

**Erro 1 — Usar exit 1 em vez de exit 2 nos bloqueios de segurança**
Exit 1 apenas avisa. Exit 2 impõe. Todo hook de bloqueio deve usar exit 2.

**Erro 2 — Hooks síncronos lentos**
Hooks que demoram mais de 500ms fazem cada chamada de ferramenta parecer lenta.
Mantenha os hooks rápidos. Use `"async": true` para logs e notificações.

**Erro 3 — Hooks muito abrangentes**
Usar `"*"` como matcher dispara em absolutamente toda chamada de ferramenta.
Seja específico: `"Edit|Write"` não `"*"`.

**Erro 4 — Instalar hooks de bloqueio globalmente sem testar**
Teste no nível de projeto primeiro. Um hook de bloqueio quebrado pode tornar
o Claude Code inutilizável. Teste com `/hooks` antes de ir global.

---

Licença MIT · Copyright (c) 2026 Caio George Santos
