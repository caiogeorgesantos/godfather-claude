# 🤵 buildflow

> *"Construa como um time de 50. Trabalhe como um time de um."*

**Um framework completo para construir produtos com agentes de IA — do zero ao infinito.**

**Autônomo · Eficiente em tokens · Seguro · Escalável**

---

## O que é o buildflow

O buildflow é um framework operacional para construir produtos com agentes de IA no Claude Code. Ele cobre o ciclo de vida completo do produto — da primeira ideia ao monitoramento e evolução contínua.

Ele define **como trabalhar** — não o que trabalhar. Cada projeto define seu próprio escopo.

Ele resolve os problemas centrais do desenvolvimento assistido por IA: sem estrutura antes de construir, agentes que saem dos trilhos, código que quebra outros códigos, squads sem memória, e produtos que vão para produção sem qualidade.

---

## A Regra de Ouro

```
REVERSÍVEL   → execute + registre no MEMORY.md + reporte no resumo da sessão
IRREVERSÍVEL → pare + descreva a ação pretendida + aguarde aprovação do Diretor
```

---

## As 11 Fases — Do Zero ao Infinito

```
FASE 0  — IDEIA
          Brainstorm estruturado. Transforma um pensamento bruto
          em uma hipótese testável que vale pesquisar.
          Ferramenta: claude.ai
          Entregável: documento de hipótese

FASE 1  — PESQUISA
          Squad de pesquisa profunda rodando em paralelo.
          Valida hipóteses com dados reais.
          Ferramenta: claude.ai (research squad)
          Entregável: relatório de pesquisa validado
          Doc: PT-BUILDFLOW-RESEARCH.md ✅

FASE 2  — VALIDAÇÃO
          Testa com mercado real antes de construir qualquer coisa.
          Landing pages, entrevistas, pré-vendas, protótipos.
          Ferramenta: claude.ai + ferramentas externas
          Entregável: go / no-go com dados reais

FASE 3  — ESPECIFICAÇÃO
          Traduz a ideia validada em spec de produto sem ambiguidade.
          Elimina o que a IA decide quando você não diz.
          Ferramenta: claude.ai
          Entregável: SPEC.md aprovado pelo Diretor

FASE 4  — BRAND
          Constrói a identidade da marca usando a pesquisa validada.
          Quem é a marca, como fala, o que nunca faz.
          Ferramenta: claude.ai
          Entregável: guia de marca

FASE 5  — PLANEJAMENTO
          Define como construir: arquitetura, fases, dependências.
          Ferramenta: claude.ai + Claude Code
          Entregável: ARCH.md aprovado pelo Diretor

FASE 6  — DESIGN
          UX, UI, acessibilidade, design system, mockups.
          Nenhuma tela é codificada sem mockup aprovado.
          Ferramenta: claude.ai + v0.dev
          Entregável: mockups aprovados

FASE 7  — EXECUÇÃO
          Constrói o produto módulo por módulo.
          Arquiteto → Dev → Auditor → QA → Segurança.
          Ferramenta: Claude Code
          Entregável: produto construído, auditado, testado
          Doc: PT-BUILDFLOW-DEV.md ✅

FASE 8  — LANÇAMENTO
          Deploy controlado em produção.
          Checklist, monitoramento, plano de rollback.
          Ferramenta: Claude Code + ferramentas externas
          Entregável: produto em produção

FASE 9  — MONITORAMENTO
          Inteligência contínua sobre mercado, concorrência,
          tecnologia, comportamento do usuário e qualidade da entrega.
          Ferramenta: claude.ai
          Entregável: relatório de inteligência periódico

FASE 10 — EVOLUÇÃO
          Transforma monitoramento em decisões de produto.
          Reinicia o ciclo na Fase 3 ou 4 com dados reais.
          Ferramenta: claude.ai + Claude Code
          Entregável: decisão de evolução aprovada + briefing
```

O produto nunca para. A Fase 10 alimenta de volta a Fase 3 ou 4 — sempre informada por dados reais do monitoramento.

---

## Módulos do framework

| Módulo | Arquivo | Fase | Status |
|--------|---------|------|--------|
| Global | `PT-BUILDFLOW-GLOBAL.md` | Todas | ✅ |
| Orquestrador | `PT-BUILDFLOW-ORCHESTRATOR.md` | Todas | ✅ |
| Agente | `PT-BUILDFLOW-AGENT.md` | Todas | ✅ |
| Template de Projeto | `PT-BUILDFLOW-PROJECT-TEMPLATE.md` | Todas | ✅ |
| Pesquisa | `PT-BUILDFLOW-RESEARCH.md` | Fase 1 | ✅ |
| Dev | `PT-BUILDFLOW-DEV.md` | Fase 7 | ✅ |
| Hooks | `PT-BUILDFLOW-HOOKS.md` | Todas | ✅ opcional |
| Ideia | `BUILDFLOW-IDEA.md` | Fase 0 | ⏳ construir quando precisar |
| Validação | `BUILDFLOW-VALIDATE.md` | Fase 2 | ⏳ construir quando precisar |
| Especificação | `BUILDFLOW-SPEC.md` | Fase 3 | ⏳ construir quando precisar |
| Brand | `BUILDFLOW-BRAND.md` | Fase 4 | ⏳ construir quando precisar |
| Planejamento | `BUILDFLOW-PLAN.md` | Fase 5 | ⏳ construir quando precisar |
| Design | `BUILDFLOW-DESIGN.md` | Fase 6 | ⏳ construir quando precisar |
| Lançamento | `BUILDFLOW-LAUNCH.md` | Fase 8 | ⏳ construir quando precisar |
| Monitoramento | `BUILDFLOW-MONITOR.md` | Fase 9 | ⏳ construir quando precisar |
| Evolução | `BUILDFLOW-EVOLVE.md` | Fase 10 | ⏳ construir quando precisar |

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
    ├── CLAUDE.md                  → Identidade do Orquestrador
    ├── BUILDFLOW-PROJECT.md       → Mapa de agentes e fluxo do projeto
    ├── SPEC.md                    → O que será construído (Fase 3)
    ├── ARCH.md                    → Como será construído (Fase 5)
    ├── MEMORY.md                  → Memória viva
    ├── DECISIONS.md               → Registro permanente de decisões
    ├── STATUS.md                  → Painel de controle da squad
    ├── _briefings/
    ├── _templates/
    └── nome-do-agente/
        ├── CLAUDE.md
        ├── MEMORY.md
        └── DECISIONS.md
```

---

## Como o PT-BUILDFLOW-DEV.md funciona (Fase 7)

O módulo mais maduro — construído a partir de experiência real em projetos.

### O fluxo de desenvolvimento por módulo

```
1. Arquiteto define ARCH.md
         ↓
2. Diretor aprova ARCH.md
         ↓
3. Arquiteto roda /plan para cada módulo
   → lista arquivos exatos para criar, modificar, reutilizar
         ↓
4. Diretor aprova Plano do Módulo
         ↓
5. Desenvolvedor constrói usando writers especializados:
   component-writer · action-writer · hook-writer
   integration-writer · model-writer · route-writer · test-writer
         ↓
6. Auditor de Código revisa — cruza com o Plano do Módulo
         ↓
7. QA Tester testa caminho feliz + edge cases + estados de falha
         ↓
8. Merge da branch para main
         ↓
9. Repete para o próximo módulo
         ↓
10. Revisor de Segurança libera para produção
         ↓
11. Lança
```

### Quality Gates — nada passa sem estes

| Gate | Quem aprova | O que bloqueia |
|------|------------|----------------|
| SPEC.md aprovado | Diretor | Nada é construído |
| ARCH.md aprovado | Diretor | Nenhum código é escrito |
| Plano do Módulo aprovado | Diretor | Desenvolvedor não começa |
| Módulo auditado | Auditor de Código | Módulo não vai para QA |
| Módulo testado | QA Tester | Módulo não faz merge |
| Segurança liberada | Revisor de Segurança | Nada vai para produção |

---

## Instalação

**Passo 1** — Salve todos os arquivos `.md` em `~/Documents/Claude/`

**Passo 2** — Para cada projeto, copie `PT-BUILDFLOW-PROJECT-TEMPLATE.md` para a raiz do projeto e renomeie para `BUILDFLOW-PROJECT.md`

**Passo 3** — Adicione este bloco ao `CLAUDE.md` do seu Orquestrador:
```markdown
## Leitura obrigatória
Antes de qualquer ação, leia nesta ordem:
1. ~/Documents/Claude/PT-BUILDFLOW-GLOBAL.md
2. ~/Documents/Claude/PT-BUILDFLOW-ORCHESTRATOR.md
3. ./BUILDFLOW-PROJECT.md
```

**Passo 4** — Adicione este bloco ao `CLAUDE.md` de cada agente:
```markdown
## Leitura obrigatória
Antes de qualquer ação, leia nesta ordem:
1. ~/Documents/Claude/PT-BUILDFLOW-GLOBAL.md
2. ~/Documents/Claude/PT-BUILDFLOW-AGENT.md
3. ./BUILDFLOW-PROJECT.md
```

**Passo 5** — Para projetos novos, comece pelo BUILDFLOW-RESEARCH. Preencha o Formulário de Pré-Projeto. Rode a squad de pesquisa no claude.ai. Avance pelas fases em ordem.

---

## Versão em Português

Todos os documentos estão disponíveis em português na pasta `/pt-br/`.

---

## O que torna o buildflow diferente

| Funcionalidade | Outros frameworks | buildflow |
|----------------|-------------------|-----------|
| Cobertura do ciclo de vida | Apenas execução | Do zero ao infinito — 11 fases |
| Pesquisa pré-projeto | Ausente | Obrigatória — Fase 1 |
| Validação de mercado | Ausente | Fase 2 antes de construir |
| Brand como fase | Ausente | Fase 4 — após validação |
| Fase de arquitetura | Implícita | Explícita — ARCH.md antes do código |
| Planejamento de módulo | Ausente | /plan por módulo — arquivos exatos listados |
| Writers especializados | Ausente | 7 tipos de writer por categoria de arquivo |
| Git branching | Raramente aplicado | Branch por módulo — obrigatório |
| Auditoria de código | Rara | Obrigatória após todo módulo |
| Testes de QA | Opcionais | Obrigatórios após toda auditoria |
| Revisão de segurança | Rara | Obrigatória antes de todo deploy |
| Memória entre sessões | Varia | MEMORY.md + DECISIONS.md padrão |
| Monitoramento e evolução | Ausente | Fases 9 e 10 — loop contínuo |

---

## Base de pesquisa

O buildflow foi construído a partir de:
- Anthropic Engineering — How we built our multi-agent research system (2025)
- Anthropic — Claude Code Best Practices (2026)
- shanraisshan/claude-code-best-practice — GitHub (2026)
- Addy Osmani — How to write a good spec for AI agents (2026)
- Deborah Folloni — Meu novo workflow Claude Code + Epic CLI (2026)
- oh-my-claudecode, Everything-Claude-Code, SuperClaude
- Experiência real em projetos — SEO, sistemas e desenvolvimento de produtos (2026)

---

## Autor

**Caio George Santos**

---

## Licença

MIT — livre para usar, modificar e distribuir com atribuição.

Copyright (c) 2026 Caio George Santos

---

*Construa como um time de 50. Trabalhe como um time de um.* 🤵
