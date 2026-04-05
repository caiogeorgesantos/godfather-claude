# 🤵 buildflow
# Módulo: RESEARCH (PESQUISA)
# Versão: 1.0 · 2026
# Uso: Antes de qualquer projeto começar. Sem exceções.

> *"Nunca tome uma decisão baseada em estimativas quando existem dados reais."*

---

## O que é este módulo

BUILDFLOW-RESEARCH é o protocolo para a Fase 1 do framework buildflow.
Roda inteiramente no claude.ai — não no Claude Code.
Termina com um entregável: relatório de pesquisa validado por área.
O relatório alimenta a Fase 3 (Especificação) onde o SPEC.md é produzido.
Nada é especificado até que o relatório de pesquisa esteja completo e revisado.

Fases do framework para referência:
- Fase 0 — IDEIA · Fase 1 — PESQUISA (este módulo) · Fase 2 — VALIDAÇÃO
- Fase 3 — ESPECIFICAÇÃO · Fase 4 — BRAND · Fase 5 — PLANEJAMENTO · Fase 6 — DESIGN
- Fase 7 — EXECUÇÃO · Fase 8 — LANÇAMENTO · Fase 9 — MONITORAMENTO · Fase 10 — EVOLUÇÃO

---

## O Formulário de Pré-Projeto

Este formulário é o seu guardrail. Preencha antes de falar com qualquer IA.
Ele te força a pensar no nível máximo desde o início.
Respostas incompletas = pesquisa incompleta = produto quebrado.

---

### BLOCO 1 — A Visão

```
Nome do projeto:
Uma frase descrevendo o que é:
Uma frase descrevendo qual problema resolve:
Quem usa (seja específico — não "pessoas", mas quem exatamente):
Como é o sucesso em 6 meses (métrica concreta):
Como é o fracasso (o que te faria abandonar o projeto):
```

### BLOCO 2 — O Negócio

```
Como este produto ganha dinheiro:
Existe um modelo de receita secundário:
Qual é o modelo de precificação (assinatura / único / freemium / B2B):
Quem paga (o usuário, um terceiro, anunciantes):
Que dados existentes você tem que são relevantes
(banco de leads, histórico de vendas, Google Ads, GSC, CRM, outros):
Que dados de conversão existem (o que converte, o que não converte):
```

### BLOCO 3 — O Mercado

```
Quais são os 3 principais concorrentes (nomeie-os, não diga "não sei"):
O que os concorrentes fazem bem que você precisa igualar:
O que os concorrentes fazem mal que é sua oportunidade:
Existe uma referência global (fora do Brasil) que faz isso bem:
Qual é o tamanho realista do mercado (não estime — se não sabe, diga):
```

### BLOCO 4 — A Marca

```
Existe guia de marca / style guide: (sim/não — se sim, anexe)
Qual é o tom de voz da marca:
O que a marca absolutamente NÃO faz ou diz:
Que referências visuais te inspiram (sites, apps, produtos):
Existe logo: (sim/não)
Existe paleta de cores: (sim/não)
```

### BLOCO 5 — Contexto Técnico

```
Existe sistema que precisa se integrar a este: (sim/não — se sim, descreva)
Existe banco de dados existente: (sim/não — se sim, o que tem nele)
Existe código existente: (sim/não — se sim, qual linguagem/framework)
Existe domínio: (sim/não)
Existe hospedagem: (sim/não — se sim, onde)
Qual é o budget para infraestrutura por mês (aproximado):
```

### BLOCO 6 — Restrições

```
Qual é o prazo de lançamento (se houver):
O que não pode mudar em hipótese alguma:
O que requer revisão legal/compliance/regulatória:
Quem precisa aprovar antes de qualquer coisa ir ao ar:
Qual é o processo de revisão de conteúdo (quem valida antes de publicar):
```

### BLOCO 7 — Padrão de Qualidade

```
Qual é a referência global de qualidade que você quer igualar ou superar:
O que te faria dizer "este é o melhor do Brasil":
O que te faria dizer "este é o melhor do mundo":
Você está disposto a atrasar o lançamento para atingir esse nível: (sim/não)
```

---

## Regras Obrigatórias Antes de Iniciar a Pesquisa

Antes de qualquer IA de pesquisa começar a trabalhar, confirme:

- [ ] Todos os 7 blocos do formulário estão preenchidos
- [ ] Todos os dados existentes foram compartilhados (GSC, Supabase, Ads, CRM)
- [ ] Guia de marca foi lido (se existir)
- [ ] Dados de conversão foram analisados (se existirem)
- [ ] Volumes reais de mercado serão validados — nenhuma estimativa aceita

**Se qualquer um destes estiver faltando: pare. Obtenha a informação. Então comece.**

---

## A Squad de Pesquisa — Projetos do claude.ai

Crie um Projeto no claude.ai por produto sendo pesquisado.
Faça upload do formulário preenchido como base de conhecimento do projeto.
Cada IA abaixo é um chat separado dentro desse projeto.

### Squad Padrão de Pesquisa

| IA | Papel | Entrega |
|----|-------|---------|
| IA 1 — Inteligência de Mercado | Players, benchmarks, tendências, gaps | market-intelligence.md |
| IA 2 — Usuário & Conversão | Quem converte, por que, o que bloqueia | user-conversion.md |
| IA 3 — Análise de Concorrentes | Análise profunda dos top 3-5 concorrentes | competitor-analysis.md |
| IA 4 — Pesquisa Técnica | Opções de stack, riscos, integrações | technical-research.md |
| IA 5 — Modelo de Negócio | Modelos de receita, precificação, monetização | business-model.md |
| IA 6 — Conteúdo & Brand | Estratégia de conteúdo, tom, estrutura | content-brand.md |
| IA Consolidadora | Sintetiza todos os outputs em relatório | research-report.md |

### Regras para IAs de Pesquisa

- Cada IA lê o formulário preenchido antes de começar
- Cada IA valida dados reais antes de qualquer recomendação
- Estimativas são sinalizadas explicitamente — nunca apresentadas como fato
- Cada IA entrega seu output como arquivo, não apenas como resposta no chat
- Nenhuma IA começa a codar ou especificar soluções — apenas pesquisa

### Template de Briefing para Cada IA de Pesquisa

```
Você é um especialista de nível mundial em [domínio].
Sua missão: pesquisar [tópico específico] para o seguinte projeto.

Leia o Formulário de Pré-Projeto anexado a este projeto antes de tudo.

Requisitos de pesquisa:
- Vá fundo. Leia artigos completos, não resumos.
- Valide todos os números com fontes reais.
- Sinalize qualquer coisa que seja estimativa, não fato.
- Foque no que é acionável, não teórico.

Fontes obrigatórias a consultar:
- [liste URLs específicas, bancos de dados ou ferramentas relevantes ao domínio]

Output:
- Salve como [nome-do-arquivo].md neste projeto
- Estrutura: descobertas → implicações → recomendações
- Toda recomendação deve ser justificada com dados

NÃO comece a escrever código ou especificações.
NÃO tome decisões — apresente descobertas para a IA Consolidadora.
```

---

## A IA Consolidadora

Após todas as IAs de pesquisa entregarem seus outputs, a Consolidadora roda.
A Consolidadora sintetiza tudo em um relatório de pesquisa — não em SPEC.md.
O SPEC.md é produzido na Fase 3 (Especificação), usando este relatório como input.

Briefing:
```
Você é a Consolidadora. Leia todos os outputs de pesquisa deste projeto.
Sua missão: produzir um relatório de pesquisa consolidado que alimentará
a fase de Especificação (Fase 3) do framework buildflow.

O relatório consolidado deve conter:
1. Resumo de mercado — players-chave, gaps, oportunidades validadas com dados
2. Perfil do usuário — quem converte, por que, o que bloqueia
3. Análise de concorrentes — o que fazem bem, o que não fazem, nossos gaps
4. Modelo de negócio — opções de receita validadas e benchmarks de precificação
5. Paisagem técnica — opções de stack, riscos, integrações disponíveis
6. Sinais de conteúdo e marca — linguagem que os usuários usam, tom que ressoa
7. Decisões-chave pendentes — o que ainda precisa ser resolvido antes da especificação
8. Registro de riscos — o que pode dar errado e como mitigar

Regras:
- Toda descoberta deve ser rastreável a um output de pesquisa
- Sem estimativas — apenas dados validados
- Sem suposições — sinalize desconhecidos explicitamente
- Sinalize contradições entre outputs de pesquisa
- Máximo 400 linhas — se precisar de mais, divida por área

Quando concluir, apresente o relatório para revisão do Diretor.
O Diretor usará isso para avançar para a Fase 2 (Validação) ou
diretamente para a Fase 3 (Especificação) se a validação não for necessária.
```

---

## Critérios de Qualidade para Entrega de Pesquisa

Um output de pesquisa é aprovado quando:
- Baseado em dados reais, não estimativas
- Toda recomendação tem justificativa
- Sem contradições com outros outputs de pesquisa
- Acionável — não apenas teórico
- Pronto para informar o relatório consolidado diretamente

Um output de pesquisa é rejeitado quando:
- Usa estimativas apresentadas como fatos
- Contradiz dados de outros outputs
- É superficial (apenas descobertas de superfície)
- Não pode ser usado diretamente para escrever o relatório consolidado

---

## O Handoff para a Próxima Fase

A pesquisa termina quando:
- [ ] Todas as IAs de pesquisa entregaram seus outputs
- [ ] Relatório de pesquisa consolidado foi produzido
- [ ] Diretor revisou e aprovou o relatório de pesquisa
- [ ] Decisões-chave pendentes foram anotadas para a Fase 2 ou Fase 3

O relatório consolidado vai para a base de conhecimento do projeto no claude.ai.
Ele alimenta a Fase 2 (Validação) ou a Fase 3 (Especificação) diretamente.
O SPEC.md é produzido na Fase 3 — não aqui.

---

## Erros Comuns — Aprenda com Projetos Reais

**Erro 1 — Priorizar sem dados reais**
Volumes estimados levaram a prioridades erradas. Sempre valide com ferramentas reais
antes de definir o que construir primeiro.

**Erro 2 — Ler o guia de marca tarde**
O guia de marca mudou toda a arquitetura quando lido no dia 3.
Leia antes de qualquer estrutura ser definida.

**Erro 3 — Ignorar dados de conversão existentes**
Dados de conversão revelaram que algumas categorias de conteúdo convertem 0%.
Analise dados existentes antes de planejar novos conteúdos ou funcionalidades.

**Erro 4 — Briefar IAs de pesquisa com escopo excessivo**
Uma IA de pesquisa sobrecarregada trava e entrega output incompleto.
Mantenha cada IA focada em um domínio. Melhor adicionar uma IA extra
do que sobrecarregar uma.

**Erro 5 — Pular o modelo de negócio**
Monetização veio do Diretor, não da pesquisa.
O modelo de negócio deve ser pesquisado e validado, não assumido.

---

Licença MIT · Copyright (c) 2026 Caio George Santos
