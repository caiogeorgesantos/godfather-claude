# BUILDFLOW-DEV
# Fase 7 do framework buildflow. Protocolo de desenvolvimento com Claude Code.
# Versão: 3.0 · 2026
# Carregado sob demanda via @referência, não toda sessão.

> *"Uma base bem feita previne retrabalho exponencial."*

---

## Critérios de entrada — antes de abrir Claude Code

- [ ] SPEC.md existe e foi aprovado pelo Diretor
- [ ] ARCH.md existe e foi aprovado pelo Diretor
- [ ] Stack definida
- [ ] Questões abertas do SPEC.md resolvidas
- [ ] Repositório Git criado com branch main
- [ ] BUILDFLOW-PROJETO.md configurado como CLAUDE.md do projeto

**Se qualquer item estiver faltando: não comece. Resolva primeiro.**

---

## SPEC.md e ARCH.md — projetos novos vs existentes

**Projeto novo:** crie SPEC.md e ARCH.md completos antes de qualquer código.

**Projeto existente:** NÃO duplique documentação. Crie wrappers enxutos (~100 linhas):

```
SPEC.md (wrapper)
- O que é este produto (2-3 linhas)
- Links para docs de spec existentes
- O que está FORA do escopo
- Critérios de qualidade
- Gate: Diretor aprova antes de qualquer módulo

ARCH.md (wrapper)
- Stack (1 linha cada)
- Links para docs técnicos existentes
- Lista de módulos na ordem de execução
- Gate: Diretor aprova antes de qualquer código
```

---

## Plano do Módulo — o guardrail mais importante

Antes de construir qualquer módulo, produza um Plano do Módulo:

```
PLANO DO MÓDULO — [nome]
Branch: feature/[nome-do-modulo]

O que faz: [uma frase]

Arquivos a CRIAR:
- [caminho] — [o que contém]

Arquivos a MODIFICAR:
- [caminho] — [o que muda e por quê]

Arquivos a REUTILIZAR:
- [caminho] — [como será usado]

Comportamentos:
- Caminho feliz: [o que acontece quando funciona]
- Edge cases: [o que acontece nos limites]
- Erros: [o que acontece quando falha]
```

**Regra: se um arquivo não está no plano, não toque nele.** Esta é a regra mais importante para prevenir IA desobediente.

Diretor aprova o Plano antes da construção começar.

---

## Quality Gates

| Gate | Quem aprova | O que bloqueia |
|------|------------|----------------|
| SPEC.md aprovado | Diretor | Nada é construído |
| ARCH.md aprovado | Diretor | Nenhum código é escrito |
| Plano do Módulo aprovado | Diretor | Construção não começa |
| Módulo auditado | Review (segunda sessão) | Módulo não vai para QA |
| Segurança verificada | Review antes de produção | Nada vai para produção |

**Para review de código:** abrir uma segunda sessão Claude Code dedicada a revisar. O agente que construiu NÃO revisa seu próprio trabalho (viés de auto-elogio).

**Para segurança:** verificar antes de todo deploy em produção:
- Chaves de API em variáveis de ambiente (nunca no código)
- Input do usuário validado e sanitizado
- Queries protegidas contra injeção
- Lógica de negócio no servidor, nunca no cliente
- Mensagens de erro sem expor detalhes internos

---

## Disciplina de Git

### Branch por módulo

```bash
git checkout main && git pull origin main
git checkout -b feature/[nome-do-modulo]
# trabalha na branch
# quando QA passar:
git checkout main && git merge feature/[nome-do-modulo]
git push origin main && git branch -d feature/[nome-do-modulo]
```

Nada faz merge para main sem aprovação do Diretor.

### Formato de commit

```
feat: [módulo] — [o que foi construído]
fix: [módulo] — [o que foi corrigido]
```

### Por que importa

Se um módulo quebrar, reverte a branch — não o projeto inteiro. Main sempre funciona.

---

## Gerenciamento de contexto

- **`/compact` a 50%** do contexto. Não espere o auto-compact. Ao compactar, diga o que preservar.
- **`/clear` ao trocar de módulo** completamente diferente.
- **Nunca misture planejamento e execução** na mesma sessão.
- **Se o agente contradizer decisões anteriores:** contexto degradou. Inicie nova sessão com CLAUDE.md re-ancorado.
- **Se o contexto degradar:** é mais barato reiniciar do que corrigir.
- **Uma tarefa por sessão.** Sessão focada > sessão longa.

---

## Agent Teams — quando escalar

Use Agent Teams quando tarefas são genuinamente paralelas e independentes. Exemplos: frontend + backend + testes simultaneamente, pesquisa em múltiplas direções, review de múltiplos módulos.

**NÃO use para:** tarefas sequenciais, edições no mesmo arquivo, tarefas simples onde o overhead não justifica.

### Como ativar

Requisito: feature flag `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS: 1` no `settings.json`. Requer Opus 4.6.

### Como usar

Descreva a tarefa e a composição do time em linguagem natural:

```
Crie um agent team com 3 membros:
- Frontend: implementar componentes de [módulo] em [stack]
- Backend: criar endpoints de API para [módulo]
- Testes: escrever testes de integração para ambos
Cada um trabalha na sua branch. Ninguém toca arquivos do outro.
```

### Custo

Agent Teams consomem 3-7x mais tokens que sessão única. Use com intenção.

### Regras

- Cada teammate recebe escopo claro e restrição de arquivos
- A Golden Rule se aplica a todos os teammates
- O Diretor pode interagir diretamente com qualquer teammate
- Prefira tmux split panes para ver todos trabalhando simultaneamente

---

## Padrão de entrega

**Aprovado quando:**
- Faz exatamente o que o SPEC.md descreve
- Segue a estrutura do ARCH.md
- Corresponde ao Plano do Módulo arquivo por arquivo
- Passou por review em sessão separada
- Não tem problemas críticos de segurança

**Rejeitado quando:**
- Faz algo que o SPEC.md não especificou
- Toca arquivos que não estavam no Plano
- Duplica código que já existia
- Foi construído sem Plano do Módulo

A pergunta antes de todo lançamento: **"Se isso falhar, eu ficaria confortável explicando por que lançamos mesmo assim?"** Se não — não lance.

---

## Radar de eficiência — revisão semanal

Uma vez por semana, avalie o projeto:

| Detectado | Ação |
|-----------|------|
| Mesmo tipo de módulo construído duas vezes | Criar template reutilizável |
| Mesmo bug em múltiplos módulos | Adicionar regra ao review |
| Agente tocando arquivos fora do plano | Reforçar disciplina do Plano do Módulo |
| Agente duplicando código existente | Adicionar regra "buscar antes de criar" |
| Agente ignorando SPEC.md | SPEC.md está longo demais — dividir |
| Contexto repetido manualmente pelo Diretor | Adicionar ao CLAUDE.md ou criar Skill |
| Tarefa executada pela 2ª vez | Criar Skill ou slash command |

---

## Erros comuns

**Codar antes da arquitetura.** Tudo é reescrito depois. ARCH.md sempre vem primeiro.

**Pular o Plano do Módulo.** Agente toca arquivos que não deveria. Uma coisa quebra outra.

**Construir tudo em uma sessão.** Contexto enche, agente perde foco. Um módulo por sessão.

**Não buscar código existente.** Cria componente que já existe. Agora tem dois. Depois três.

**Pular review porque "parece certo".** 45% do código gerado por IA contém vulnerabilidades. "Parece certo" não é padrão de qualidade.

**Testar só o caminho feliz.** Funciona em demo, quebra com usuários reais.

**Deploy sem review de segurança.** Lógica de negócio no frontend. Chaves no código.

**Merge direto para main.** Algo quebra e afeta tudo. Branch por módulo. Main sempre limpa.

---

MIT License · Copyright (c) 2026 Caio George Santos
