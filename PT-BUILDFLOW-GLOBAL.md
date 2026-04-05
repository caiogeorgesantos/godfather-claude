# 🤵 buildflow
# Documento: GLOBAL · Versão: 1.0
# Lido por: TODOS os agentes, toda sessão

> *"Construa como um time de 50. Trabalhe como um time de um."*

---

## O que é o buildflow

Um framework completo para construir produtos com agentes de IA — do zero ao infinito.
Define **como trabalhar** — não o que trabalhar.
Cada projeto tem seu próprio BUILDFLOW-PROJECT.md que define o que trabalhar.

---

## Dois modos de operação — escolha antes de começar

### Modo 1 — Agente Único
Uma conversa, um agente, execução direta.

**Use quando:** founder solo sem janelas paralelas, iteração rápida necessária, um agente ativo por vez.

**O que usar:** SPEC.md, ARCH.md, DECISIONS.md, STATUS.md, MEMORY.md, BUILDFLOW-PROJECT.md. Planos de Módulo apenas para features complexas.

**O que ignorar:** protocolo de squad, briefings, handoffs, pastas de agente.

### Modo 2 — Squad Multi-Agente
Múltiplas janelas do VS Code, agentes especializados em paralelo.

**Use quando:** tarefas genuinamente paralelas e independentes, volume excede uma janela de contexto.

**O que usar:** framework completo — todos os protocolos ativos. Planos de Módulo e branches Git obrigatórios por módulo.

**Declare o modo no BUILDFLOW-PROJECT.md antes de qualquer trabalho.**

Bloco de leitura obrigatória para todo CLAUDE.md:
```
Antes de qualquer ação, leia nesta ordem:
1. ~/Documents/Claude/PT-BUILDFLOW-GLOBAL.md
2. ~/Documents/Claude/PT-BUILDFLOW-ORCHESTRATOR.md  ← Somente Orquestrador
3. ~/Documents/Claude/PT-BUILDFLOW-AGENT.md          ← Somente Agentes
4. ./BUILDFLOW-PROJECT.md                         ← Contexto deste projeto
```

---

## Estrutura de pastas

```
~/Documents/Claude/
├── PT-BUILDFLOW-GLOBAL.md
├── PT-BUILDFLOW-ORCHESTRATOR.md
├── PT-BUILDFLOW-AGENT.md
├── PT-BUILDFLOW-RESEARCH.md
├── PT-BUILDFLOW-DEV.md
├── PT-BUILDFLOW-HOOKS.md         ← Gates de segurança (opcional)
│
└── seu-projeto/
    ├── CLAUDE.md                → Identidade do Orquestrador
    ├── BUILDFLOW-PROJECT.md     → Mapa de agentes e fluxo do projeto
    ├── SPEC.md                  → O que será construído (Fase 3)
    ├── ARCH.md                  → Como será construído (Fase 5)
    ├── MEMORY.md                → Memória viva — atualizada toda sessão
    ├── DECISIONS.md             → Registro permanente de decisões — nunca deletado
    ├── STATUS.md                → Painel de controle da squad
    ├── _briefings/
    ├── _templates/
    └── nome-do-agente/
        ├── CLAUDE.md
        ├── MEMORY.md
        └── DECISIONS.md
```

---

## Regras de escrita de instruções

- Use bullets, nunca parágrafos longos
- Seja específico: "Salve em _briefings/" não "salve no lugar certo"
- Coloque a regra mais importante primeiro em cada seção
- Mantenha todo CLAUDE.md abaixo de 200 linhas
- Acima de 200 linhas → use .claude/rules/ para arquivos modulares

---

## A Regra de Ouro

```
REVERSÍVEL   → execute + registre no MEMORY.md + reporte no resumo da sessão
IRREVERSÍVEL → pare + descreva a ação pretendida + aguarde aprovação do Diretor
```

**Reversível — age sem perguntar:**
- Criar novos arquivos
- Atualizar MEMORY.md, DECISIONS.md, STATUS.md
- Gerar briefings e handoffs
- Sugerir Skills, templates, protocolos
- Reorganizar conteúdo dentro de arquivos existentes

**Irreversível — para e pergunta:**
- Deletar qualquer arquivo ou pasta
- Modificar o CLAUDE.md de outro agente
- Publicar ou fazer deploy em produção
- Gastar dinheiro — APIs pagas, serviços externos
- Decisões que afetam múltiplos projetos
- Qualquer ação não reversível em 5 minutos

**Resumo de fim de resposta — sempre quando ações foram tomadas:**
```
✅ EXECUTADO:
- [ação] → [arquivo afetado]

⏳ AGUARDANDO APROVAÇÃO:
- [ação irreversível] → [motivo]
```

---

## Quando usar squad vs agente único

**Use agente único quando:**
- Tarefa sequencial com dependências entre etapas
- Edições no mesmo arquivo
- Trabalho que requer contexto compartilhado em tempo real
- Tarefa simples com resultado previsível

**Use squad quando:**
- Subtarefas genuinamente paralelas e independentes
- Pesquisa em múltiplas direções simultaneamente
- Volume que excede uma janela de contexto
- Módulos distintos sem dependência em tempo real

Nota: squads usam ~15x mais tokens que sessões de agente único.
Use apenas quando o valor da tarefa justificar.

---

## Arquivos padrão

### MEMORY.md
```
# MEMORY — [nome do agente]
# Atualizado: [data hora]

## Sessão atual
- Feito: [lista específica com caminhos de arquivos]
- Decisões: [resumo — detalhes no DECISIONS.md]
- Pendente: [lista]

## Estado do projeto
[resumo em até 8 linhas]

## Próximo passo
[uma ação específica e clara]
```

### DECISIONS.md
```
# DECISIONS — [projeto/agente]

## [data] — [título da decisão]
- Contexto: [por que surgiu]
- Decisão: [o que foi decidido]
- Motivo: [por que esta opção]
- Impacto: [o que muda]
```

### STATUS.md — mantido pelo Orquestrador
```
# STATUS — [projeto] | Atualizado: [data]

| Agente | Último trabalho | Status         | Próximo passo |
|--------|-----------------|----------------|---------------|
| [nome] | [data]          | ✅ concluído   | [ação]        |
| [nome] | [data]          | 🔄 em progresso| [ação]        |
| [nome] | [data]          | ⏸️ pausado     | [ação]        |
| [nome] | [data]          | ⚠️ bloqueado   | [ação]        |
```

---

## Padrões de nomenclatura de arquivos

```
briefing_[agente]_[AAAAMMDD].md
handoff_[de]_[para]_[AAAAMMDD].md
auditoria_[agente]_[AAAAMMDD].md
template_[nome].md
```

---

## Radar de Eficiência

Avalie ao final de cada resposta. Sinalize apenas quando genuíno.

| Situação detectada | Ação recomendada |
|---|---|
| Tarefa executada pela 2ª vez ou mais | Crie uma Skill |
| Contexto explicado manualmente pelo Diretor | Adicione ao CLAUDE.md |
| Briefing seguindo padrão recorrente | Crie um template fixo |
| Mesmo fluxo multi-agente repetido | Crie um protocolo documentado |
| Consulta externa recorrente | Avalie MCP ou integração |
| Decisão importante tomada em conversa | Registre no DECISIONS.md agora |
| Novo tipo de agente mencionado | Crie pasta e CLAUDE.md |

```
💡 RADAR DE EFICIÊNCIA
Detectado: [o que foi identificado]
Padrão: [por que parece recorrente]
Recomendo: [Skill / template / protocolo / CLAUDE.md / novo agente]
Impacto esperado: [o que economiza]
→ Criar agora ou registrar como pendente?
```

---

## Checklist de encerramento de sessão — obrigatório toda sessão

```
□ MEMORY.md atualizado
□ Decisões importantes no DECISIONS.md
□ STATUS.md atualizado (se aplicável)
□ Próximo passo documentado
□ Resumo de execução entregue ao Diretor
□ Radar de Eficiência avaliado
```

Confirmação de encerramento:
```
📋 ENCERRAMENTO DE SESSÃO
Agente: [nome] | Projeto: [nome] | Data: [data]

✅ Feito: [lista]
📝 Registrado: [MEMORY / DECISIONS / STATUS]
⏭️ Próximo passo: [ação específica]
⚠️ Aguardando aprovação: [lista ou Nenhum]
```

---

## Escalada ao Diretor

Escale quando:
- Ação é irreversível
- Briefing é ambíguo ou incompleto
- Conflito entre o framework e o CLAUDE.md do projeto
- Resultado esperado não está claro
- Algo inesperado aconteceu

```
🚨 ESCALADA
Agente: [nome]
Situação: [o que está bloqueando]
Opções:
  A) [opção] → [consequência]
  B) [opção] → [consequência]
Recomendação: [opção sugerida e por quê]
→ Qual caminho?
```

---

## Quando ativar o Auditor

- Semanalmente — auditoria de rotina da squad
- Antes de novo projeto multi-agente
- Quando um agente entrega resultados inconsistentes
- Após sessões longas com muitas decisões
- Quando há dúvida sobre responsabilidades sobrepostas

---

Licença MIT · Copyright (c) 2026 Caio George Santos
