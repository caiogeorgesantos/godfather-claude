# 🤵 BUILDFLOW
# Framework para construir produtos com agentes de IA — do zero ao infinito.
# Versão: 3.0 · 2026 · Caio George Santos · MIT License
# Este documento é referência. Não é lido automaticamente toda sessão.
# O documento operacional é o BUILDFLOW-PROJETO.md de cada projeto.

> *"Construa como um time de 50. Trabalhe como um time de um."*

---

## O que é

Framework operacional para solo founders construírem produtos com Claude.
Define como trabalhar — não o que trabalhar.
Cada projeto tem seu próprio BUILDFLOW-PROJETO.md que define o que trabalhar.

---

## Regra de Ouro

```
REVERSÍVEL   → execute + registre no ESTADO + reporte no resumo
IRREVERSÍVEL → pare + descreva a ação + aguarde aprovação do Diretor
```

---

## As 11 Fases

| Fase | Nome | Onde roda | Entregável |
|------|------|-----------|------------|
| 0 | IDEIA | Claude.ai | Hipótese documentada |
| 1 | PESQUISA | Claude.ai | Relatório validado (ver BUILDFLOW-PESQUISA.md) |
| 2 | VALIDAÇÃO | Claude.ai + externo | Go/no-go com dados reais |
| 3 | ESPECIFICAÇÃO | Claude.ai | SPEC.md aprovado |
| 4 | BRAND | Claude.ai | Guia de marca |
| 5 | PLANEJAMENTO | Claude.ai + Code | ARCH.md aprovado |
| 6 | DESIGN | Claude.ai + v0.dev | Mockups aprovados |
| 7 | EXECUÇÃO | Claude Code | Produto construído (ver BUILDFLOW-DEV.md) |
| 8 | LANÇAMENTO | Claude Code + externo | Produto em produção |
| 9 | MONITORAMENTO | Claude.ai | Relatório de inteligência |
| 10 | EVOLUÇÃO | Claude.ai + Code | Decisão de evolução → reinicia na Fase 3 ou 4 |

O produto nunca para. Fase 10 alimenta Fase 3 ou 4 com dados reais.

---

## Onde fazer cada tipo de tarefa

| Tarefa | Ferramenta | Por quê |
|--------|-----------|---------|
| Estratégia, planejamento, brainstorming | **Claude.ai (Projects)** | Memória entre sessões, web search, integrações (Drive, Calendar, Gmail) |
| Pesquisa profunda, análise de mercado | **Claude.ai (Deep Research)** | Pesquisa web automatizada, síntese de múltiplas fontes |
| Desenvolvimento, automação, deploys | **Claude Code** | Acesso ao terminal, codebase, execução de comandos |
| Documentos complexos (.docx, .pptx, .xlsx) | **Claude Cowork** | Skills de criação de arquivos, acesso a arquivos locais |
| Organização de arquivos, tarefas desktop | **Claude Cowork** | Acesso ao filesystem, tarefas agendadas |
| Tarefas recorrentes, agendadas | **Claude Cowork (Scheduled Tasks)** | Executa mesmo sem você presente |
| Estudo e consolidação de aprendizados | **Claude.ai (Projects)** ou **NotebookLM** | Contexto persistente por tema |

Regra: não troque de ferramenta para evitar trocar. Troque quando a tarefa exige. Cada ferramenta tem força diferente.

---

## Modelo de IA — quando usar cada um

| Modelo | Custo relativo | Quando usar |
|--------|---------------|-------------|
| **Haiku** | $ | Pesquisa, classificação, tarefas simples, sub-agents de exploração |
| **Sonnet** | $$ | 80% do trabalho diário: código, documentos, análise, implementação |
| **Opus** | $$$$$ | Decisões arquiteturais, reviews complexos, Agent Teams, raciocínio profundo |

Regra: comece com Sonnet. Só escale para Opus quando o resultado com Sonnet não for suficiente.
Opus custa ~5x mais que Sonnet. Use com intenção, não por hábito.

---

## Divisão de responsabilidades

### A IA faz sozinha (automático, sem o Diretor precisar pedir):
- Entrevistar antes de tarefas complexas
- Escolher o modelo adequado para a tarefa
- Verificar completude antes de declarar "feito"
- Pedir clarificação quando o pedido é ambíguo
- Atualizar ESTADO ao final de sessões
- Alertar quando contexto está degradando (>50%)
- Não sobre-engenheirar (seguir só o escopo pedido)
- Buscar código existente antes de criar novo

### O Diretor faz (decisões humanas):
- Aprovar specs e arquiteturas antes de execução
- Review final de entregas críticas
- Decisões de negócio (priorização, go/no-go, pricing)
- Aprovar gastos (deploys, APIs pagas, serviços externos)
- Decidir quando escalar para Agent Teams
- Definir escopo e intenção de cada tarefa

### A IA sugere, Diretor decide:
- Quando iniciar nova sessão (IA alerta, Diretor decide)
- Quando escalar complexidade (IA recomenda, Diretor aprova)
- Quando um projeto precisa de mais contexto/skills

---

## Princípios de context engineering

1. **Sessões curtas e focadas.** Uma tarefa por sessão. Não reutilize sessões para tarefas diferentes.
2. **CLAUDE.md enxuto.** O BUILDFLOW-PROJETO.md deve ter menos de 120 linhas. Se crescer além disso, mova conhecimento para Skills.
3. **Skills > CLAUDE.md** para conhecimento especializado. Skills carregam sob demanda, CLAUDE.md carrega toda sessão.
4. **`/compact` a 50%.** Não espere o auto-compact a 95%. Ao compactar, diga o que preservar.
5. **`/clear` para trocar de tarefa.** Não misture planejamento e execução na mesma sessão.
6. **`.claudeignore`** para excluir node_modules, dist, lock files, build artifacts.
7. **Prompts específicos.** "Fix auth bug in src/auth.js" gasta menos tokens que "fix the bug."
8. **Se o agente contradizer decisões anteriores:** contexto degradou. Iniciar nova sessão.

---

## Instalação

1. Copie `BUILDFLOW-PROJETO.md` para a raiz de cada projeto e renomeie para `CLAUDE.md`
2. Preencha a identidade do projeto, restrições e contexto de negócio
3. Para projetos novos, comece pelo `BUILDFLOW-PESQUISA.md` no Claude.ai
4. Instale os hooks de `BUILDFLOW-HOOKS.md` no `.claude/settings.json`
5. Guarde `BUILDFLOW.md`, `BUILDFLOW-PESQUISA.md` e `BUILDFLOW-DEV.md` em `~/Documents/Claude/` como referência

---

## Licença

MIT — livre para usar, modificar e distribuir com atribuição.
Copyright (c) 2026 Caio George Santos

*Construa como um time de 50. Trabalhe como um time de um.* 🤵
