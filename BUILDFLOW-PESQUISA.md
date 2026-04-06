# BUILDFLOW-PESQUISA
# Fase 1 do framework buildflow. Roda no Claude.ai, não no Claude Code.
# Versão: 3.0 · 2026

> *"Nunca tome uma decisão baseada em estimativas quando existem dados reais."*

---

## O que é

Protocolo para Fase 1 (Pesquisa) do buildflow.
Termina com um relatório de pesquisa validado que alimenta a Fase 3 (Especificação/SPEC.md).
Nada é especificado até que a pesquisa esteja completa e revisada.

---

## Como funciona

A pesquisa começa com uma **entrevista** — a IA pergunta, o Diretor responde.
Depois, a IA pesquisa e consolida. O Diretor revisa e aprova.

```
Entrevista (7 blocos) → Pesquisa profunda → Relatório consolidado → Aprovação do Diretor → Fase 3
```

---

## Protocolo de entrevista — 7 blocos

A IA deve conduzir a entrevista usando os blocos abaixo como guia.
Não apresente o formulário inteiro de uma vez — faça bloco por bloco, conversacionalmente.
Aceite respostas parciais. Sinalize quando informação está faltando mas não bloqueie.

### Bloco 1 — Visão
- O que é este projeto?
- Que problema resolve?
- Quem usa (ser específico — não "pessoas", mas quem exatamente)?
- Como é o sucesso em 6 meses (métrica concreta)?
- O que faria você abandonar o projeto?

### Bloco 2 — Negócio
- Como este produto ganha dinheiro?
- Existe modelo de receita secundário?
- Qual o modelo de precificação (assinatura / único / freemium / B2B)?
- Quem paga (o usuário, um terceiro, anunciantes)?
- Que dados existentes são relevantes (leads, vendas, Ads, CRM, GSC)?
- Que dados de conversão existem (o que converte, o que não)?

### Bloco 3 — Mercado
- Quem são os 3 principais concorrentes (nomeie-os)?
- O que fazem bem que você precisa igualar?
- O que fazem mal que é sua oportunidade?
- Existe referência global (fora do Brasil) que faz isso bem?
- Qual o tamanho realista do mercado (não estime — se não sabe, diga)?

### Bloco 4 — Marca
- Existe guia de marca / style guide?
- Qual o tom de voz?
- O que a marca absolutamente NÃO faz ou diz?
- Que referências visuais inspiram (sites, apps, produtos)?
- Existe logo e paleta de cores?

### Bloco 5 — Contexto técnico
- Existe sistema que precisa se integrar a este?
- Existe banco de dados? O que tem nele?
- Existe código? Qual linguagem/framework?
- Existe domínio e hospedagem?
- Qual o budget para infraestrutura por mês?

### Bloco 6 — Restrições
- Qual o prazo de lançamento?
- O que não pode mudar em hipótese alguma?
- O que requer revisão legal/compliance?
- Quem precisa aprovar antes de ir ao ar?

### Bloco 7 — Padrão de qualidade
- Qual referência global de qualidade quer igualar ou superar?
- O que te faria dizer "este é o melhor do Brasil"?
- O que te faria dizer "este é o melhor do mundo"?
- Está disposto a atrasar o lançamento para atingir esse nível?

---

## Regras antes de pesquisar

Antes de iniciar a pesquisa, confirme:
- [ ] Todos os 7 blocos da entrevista foram cobertos (respostas parciais ok, desde que sinalizadas)
- [ ] Dados existentes foram compartilhados (GSC, Supabase, Ads, CRM) — se existirem
- [ ] Guia de marca foi lido — se existir
- [ ] Dados de conversão foram analisados — se existirem

Se informação crítica estiver faltando: sinalize e prossiga com o que tem. Não bloqueie.

---

## Pesquisa

Use Deep Research ou pesquisa manual para cobrir:

1. **Mercado** — players, gaps, oportunidades, tamanho real
2. **Usuário** — quem converte, por que, o que bloqueia
3. **Concorrentes** — análise profunda dos top 3-5
4. **Modelo de negócio** — opções de receita validadas, benchmarks de pricing
5. **Paisagem técnica** — opções de stack, riscos, integrações
6. **Conteúdo e marca** — linguagem que usuários usam, tom que ressoa

Regras:
- Valide números com fontes reais. Sinalize explicitamente o que é estimativa vs fato.
- Foque no que é acionável, não teórico.
- Máximo 400 linhas no relatório. Se precisar mais, divida por área.

---

## Relatório consolidado

O relatório deve conter:

1. Resumo de mercado — validado com dados
2. Perfil do usuário — quem converte e por quê
3. Análise de concorrentes — forças, fraquezas, gaps
4. Modelo de negócio — opções validadas
5. Paisagem técnica — stack recomendada com justificativa
6. Sinais de conteúdo e marca
7. **Decisões pendentes** — o que ainda precisa ser resolvido antes de especificar
8. **Riscos** — o que pode dar errado e como mitigar

Toda descoberta deve ser rastreável. Sem estimativas como fatos. Sem suposições — sinalize desconhecidos.

---

## Handoff para próxima fase

A pesquisa termina quando:
- [ ] Relatório consolidado produzido
- [ ] Diretor revisou e aprovou
- [ ] Decisões pendentes anotadas para Fase 3

O relatório vai para o Project do claude.ai como conhecimento do projeto.
Ele alimenta diretamente a Fase 3 (Especificação) onde o SPEC.md é produzido.

---

## Erros comuns

**Priorizar sem dados reais.** Volumes estimados levam a prioridades erradas. Valide com ferramentas reais antes de definir o que construir primeiro.

**Ler o guia de marca tarde.** Guia de marca pode mudar toda a arquitetura. Leia antes de qualquer estrutura.

**Ignorar dados de conversão existentes.** Dados de conversão podem revelar que categorias inteiras convertem 0%. Analise antes de planejar.

**Pular o modelo de negócio.** Monetização deve ser pesquisada e validada, não assumida.

---

MIT License · Copyright (c) 2026 Caio George Santos
