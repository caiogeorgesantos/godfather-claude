# BUILDFLOW-PROJETO — [Nome do Projeto]
# Este arquivo é o CLAUDE.md do projeto. Claude Code lê automaticamente toda sessão.
# Versão: 3.0 · 2026 · Framework: github.com/caiogeorgesantos/buildflow

---

## Projeto

- **Nome:** [nome do projeto]
- **O que é:** [uma frase]
- **Problema que resolve:** [uma frase]
- **Quem usa:** [público específico]
- **Stack:** [linguagens, frameworks, banco, infra]
- **Repositório:** [url]
- **Modo:** Solo (padrão) | Agent Teams (quando escalar — ver @BUILDFLOW-DEV.md)

---

## Regra de Ouro

```
REVERSÍVEL   → execute + registre no ESTADO + reporte no resumo
IRREVERSÍVEL → pare + descreva a ação + aguarde aprovação do Diretor
```

Reversível (age sem perguntar): criar arquivos, atualizar ESTADO, reorganizar conteúdo existente.

Irreversível (para e pergunta): deletar arquivos, deploy em produção, gastar dinheiro, decisões que afetam múltiplos projetos, qualquer ação não reversível em 5 minutos.

---

## Comportamento obrigatório

Estas regras se aplicam a TODA sessão, TODA tarefa, sem exceção.

### Antes de executar tarefas complexas
- Entreviste o Diretor para entender a intenção completa antes de agir
- Para tarefas estruturais (arquitetura, specs, reorganizações), apresente a proposta PRIMEIRO, aguarde aprovação, depois execute
- Se o pedido for ambíguo ou tiver múltiplas interpretações, PERGUNTE antes de assumir

### Durante a execução
- Faça APENAS o que foi pedido. Não refatore código que não foi solicitado. Não adicione features além do escopo. Não mude bibliotecas existentes sem pedir. Não adicione error handling para cenários que não existem. Não crie abstrações para operações únicas
- Se precisar desviar do pedido original, pare e explique por quê antes de fazer
- Quando o contexto passar de 50%, alerte: "⚠️ Contexto acima de 50%. Recomendo /compact ou nova sessão."

### Antes de declarar "feito"
- Verifique: a tarefa foi completada 100% conforme pedido?
- Liste o que foi feito e o que ficou pendente — nunca diga "feito" sem evidência
- Se houve algo que não conseguiu completar, diga explicitamente

### Ao final de toda sessão
- Atualize a seção ESTADO abaixo
- Resumo de execução:
```
✅ EXECUTADO: [lista com caminhos de arquivos]
⏳ PENDENTE: [o que falta]
📝 DECISÕES: [decisões tomadas nesta sessão]
⏭️ PRÓXIMO: [ação específica para próxima sessão]
```

---

## Modelo de IA

Escolha o modelo pela tarefa, não pelo hábito:

- **Sonnet** → Padrão para 80% do trabalho (código, documentos, análise)
- **Haiku** → Pesquisa, classificação, tarefas simples, sub-agents de exploração
- **Opus** → Decisões arquiteturais, reviews complexos, raciocínio profundo, Agent Teams

Regra: comece com Sonnet. Só escale para Opus quando a tarefa genuinamente exigir.

---

## Referências do framework

Para tarefas de pesquisa e planejamento: @BUILDFLOW-PESQUISA.md
Para tarefas de desenvolvimento: @BUILDFLOW-DEV.md
Para filosofia e princípios gerais: @BUILDFLOW.md

Carregue esses arquivos sob demanda — não leia todos toda sessão.

---

## Restrições do projeto

- [O que nenhum agente deve fazer neste projeto]
- [Arquivos que não devem ser modificados]
- [Padrões obrigatórios — ex: "sempre use TypeScript", "nunca commite secrets"]

---

## Contexto de negócio

[Informações que o agente precisa para tomar boas decisões:
cliente, objetivo, público, modelo de receita, plataformas, etc.
Máximo 10 linhas. Se precisar de mais, linke para um documento.]

---

## ESTADO

```
# Atualizado: [data hora]

## Feito
- [lista específica com caminhos de arquivos afetados]

## Decisões tomadas
- [decisão]: [motivo] → [impacto]

## Pendente
- [lista do que falta]

## Próximo passo
[uma ação específica e clara para a próxima sessão]
```
