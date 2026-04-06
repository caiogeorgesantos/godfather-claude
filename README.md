# 🤵 buildflow

> *"Construa como um time de 50. Trabalhe como um time de um."*

**Framework completo para construir produtos com agentes de IA — do zero ao infinito.**

---

## O que é

buildflow é um framework operacional para solo founders construírem produtos com Claude.
Cobre o ciclo de vida completo — da primeira ideia ao monitoramento e evolução contínua.

Define **como trabalhar** — não o que trabalhar.

Resolve os problemas reais do desenvolvimento com IA: agentes que saem dos trilhos, código que quebra outro código, contexto que se perde entre sessões, entregas incompletas, e produtos que vão para produção sem qualidade.

---

## Como funciona em 30 segundos

1. Copie `BUILDFLOW-PROJETO.md` para a raiz do projeto como `CLAUDE.md`
2. Preencha identidade do projeto (10 linhas)
3. Para projetos novos, rode `BUILDFLOW-PESQUISA.md` no Claude.ai (entrevista → pesquisa → spec)
4. Abra Claude Code — guardrails já ativos automaticamente
5. Para desenvolvimento, carregue `@BUILDFLOW-DEV.md` sob demanda

O Claude Code lê o `CLAUDE.md` toda sessão. Guardrails contra falhas da IA estão embutidos. Você não precisa lembrar de nada.

---

## As 11 Fases — do zero ao infinito

```
FASE 0  — IDEIA           Hipótese documentada
FASE 1  — PESQUISA        Relatório validado com dados reais
FASE 2  — VALIDAÇÃO       Go/no-go com mercado real
FASE 3  — ESPECIFICAÇÃO   SPEC.md aprovado
FASE 4  — BRAND           Identidade de marca
FASE 5  — PLANEJAMENTO    ARCH.md aprovado
FASE 6  — DESIGN          Mockups aprovados
FASE 7  — EXECUÇÃO        Produto construído, auditado, testado
FASE 8  — LANÇAMENTO      Produto em produção
FASE 9  — MONITORAMENTO   Inteligência contínua
FASE 10 — EVOLUÇÃO        Reinicia na Fase 3 ou 4 com dados reais
```

O produto nunca para. Fase 10 alimenta Fase 3 com dados reais do mundo.

---

## Arquivos do framework

| Arquivo | Função | Quando usar |
|---------|--------|-------------|
| `BUILDFLOW-PROJETO.md` | Template → vira CLAUDE.md do projeto | Todo projeto |
| `BUILDFLOW.md` | Princípios, fases, decisões de modelo | Referência sob demanda |
| `BUILDFLOW-PESQUISA.md` | Entrevista + pesquisa (Fase 1) | Antes de cada projeto |
| `BUILDFLOW-DEV.md` | Protocolo de desenvolvimento (Fase 7) | Quando for construir |
| `BUILDFLOW-HOOKS.md` | Gates de segurança determinísticos | Setup do projeto |

---

## O que torna o buildflow diferente

| | Outros frameworks | buildflow |
|--|-------------------|-----------|
| Ciclo de vida | Só execução | 11 fases — ideia ao infinito |
| Pesquisa pré-projeto | Ausente | Obrigatória com entrevista estruturada |
| Guardrails contra falhas da IA | Ausentes | Embutidos no CLAUDE.md (context rot, task drift, sobre-engenharia, entrega incompleta) |
| Validação de mercado | Ausente | Fase 2 antes de construir |
| Arquitetura | Implícita | Explícita — ARCH.md antes de código |
| Plano de módulo | Ausente | Obrigatório — lista exata de arquivos |
| Review de código | Rara | Obrigatória em sessão separada |
| Memória entre sessões | Varia | ESTADO.md integrado ao CLAUDE.md |
| Multi-agente | Burocrático | Agent Teams nativo do Claude Code |
| Decisão de modelo | Ausente | Haiku/Sonnet/Opus com critérios claros |
| Economia de tokens | Ignorada | Princípio de design |
| Divisão IA/humano | Implícita | Explícita — quem faz o quê |

---

## Regra de Ouro

```
REVERSÍVEL   → execute + registre + reporte
IRREVERSÍVEL → pare + descreva + aguarde aprovação
```

---

## Base de pesquisa

Construído a partir de:
- Anthropic — Claude Code Best Practices e Context Engineering (2025-2026)
- Anthropic — Harness Design for Long-Running Applications (2026)
- shanraisshan/claude-code-best-practice — GitHub (2026)
- Pesquisa acadêmica sobre failure modes de LLMs e multi-agent systems (2025-2026)
- Experiência real em projetos — SEO, sistemas, legaltech, e desenvolvimento de produtos (2025-2026)

---

## Autor

**Caio George Santos**

---

## Licença

MIT — livre para usar, modificar e distribuir com atribuição.

Copyright (c) 2026 Caio George Santos

*Construa como um time de 50. Trabalhe como um time de um.* 🤵
