# BUILDFLOW-PROJECT — [Nome do Projeto]
# Versão: 1.0 | Criado: [data] | Mantido por: Orquestrador

---

## Descrição do projeto

[Uma frase descrevendo o projeto e seu objetivo principal]

---

## Tipo de projeto

```
Tipo de projeto: [ ] Novo (começa do zero) / [ ] Existente (já tem documentação)

Se NOVO:
- SPEC.md: documento completo — criado na Fase 3
- ARCH.md: documento completo — criado na Fase 5

Se EXISTENTE:
- SPEC.md: wrapper enxuto (~100 linhas) — índice + gate apontando para docs existentes
- ARCH.md: wrapper enxuto (~100 linhas) — índice + gate apontando para docs técnicos existentes
- Documentação existente: [liste documentos-chave e suas localizações]
```

---

## Documentos-chave

| Documento | Status | Local | Responsável |
|-----------|--------|-------|-------------|
| SPEC.md | [ ] pendente / [x] aprovado | ./SPEC.md | Diretor |
| ARCH.md | [ ] pendente / [x] aprovado | ./ARCH.md | Arquiteto |
| BUILDFLOW-PROJECT.md | [x] ativo | ./BUILDFLOW-PROJECT.md | Orquestrador |
| MEMORY.md | [x] ativo | ./MEMORY.md | Orquestrador |
| DECISIONS.md | [x] ativo | ./DECISIONS.md | Todos os agentes |
| STATUS.md | [x] ativo | ./STATUS.md | Orquestrador |

**SPEC.md não aprovado → nada é especificado ou construído.**
**ARCH.md não aprovado → nenhum código é escrito.**

---

## Mapa da squad

| Agente | Pasta | Papel | Recebe de | Entrega para |
|--------|-------|-------|-----------|--------------|
| Orquestrador | ./ | Coordena a squad | Diretor | Todos os agentes |
| [Agente 1] | ./[pasta] | [papel] | [origem] | [destino] |
| [Agente 2] | ./[pasta] | [papel] | [origem] | [destino] |
| Auditor | ./auditor | Audita agentes e entregáveis | Orquestrador | Diretor |

---

## Fluxo de trabalho padrão

```
Diretor → briefing → Orquestrador
Orquestrador → mapeia agentes → gera briefings → aguarda aprovação
Diretor → aprova → Orquestrador libera
Agente 1 → executa → handoff → Agente 2
Agente 2 → executa → entrega → Orquestrador
Orquestrador → consolida → entrega → Diretor
```

---

## Quando NÃO usar squad neste projeto

- [Liste tipos de tarefa que um agente único resolve melhor]
- Exemplo: edições pontuais em um único arquivo
- Exemplo: tarefas com menos de 2h de trabalho estimado

---

## Entregáveis padrão

| Entregável | Formato | Salvar em | Responsável |
|------------|---------|-----------|-------------|
| [nome] | [.md / .html / etc] | [caminho] | [agente] |

---

## Restrições do projeto

- [O que nenhum agente deve fazer neste projeto]
- [Arquivos que não devem ser modificados]
- [Padrões obrigatórios]

---

## Contexto de negócio

[Informações que todos os agentes precisam sobre este projeto:
cliente, objetivo, público, plataformas envolvidas, etc.]

---

## Histórico de versões do BUILDFLOW-PROJECT

| Data | Mudança |
|------|---------|
| [data] | Criação inicial |

---

Licença MIT — Copyright (c) 2026 Caio George Santos
