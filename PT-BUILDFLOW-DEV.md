# 🤵 buildflow
# Módulo: DEV (DESENVOLVIMENTO)
# Versão: 2.0 · 2026
# Uso: Após SPEC.md e ARCH.md aprovados. Antes de abrir o Claude Code.

> *"Uma base bem feita previne retrabalho exponencial."*

---

## O que é este módulo

BUILDFLOW-DEV é o protocolo para construir produtos com Claude Code.
Inicia apenas após SPEC.md e ARCH.md existirem e serem aprovados.
Termina apenas quando o produto passa pelos critérios de qualidade.
Aplica-se a qualquer tipo de produto: landing pages, sistemas, apps, portais.

---

## Critérios de entrada inegociáveis

Antes de abrir o Claude Code, confirme:

- [ ] SPEC.md existe e foi aprovado pelo Diretor
- [ ] ARCH.md existe e foi aprovado pelo Diretor
- [ ] Stack foi definida
- [ ] Todas as questões abertas do SPEC.md foram resolvidas
- [ ] Arquivos do framework buildflow estão em ~/Documents/Claude/
- [ ] Repositório Git foi criado com branch main
- [ ] BUILDFLOW-PROJECT.md foi criado para este projeto

**Se qualquer um destes estiver faltando: não abra o Claude Code.**

---

## Modo de operação — confirme antes de abrir o Claude Code

Leia o BUILDFLOW-PROJECT.md para confirmar o modo:

**Modo 1 — Agente Único:**
- Arquivos de controle obrigatórios: SPEC.md + ARCH.md aprovados
- Planos de Módulo: apenas para features complexas
- Branches Git: opcionais
- Sem ativação de squad, briefings ou pastas de agente
- Prossiga diretamente para execução

**Modo 2 — Squad Multi-Agente:**
- Todos os quality gates se aplicam
- Planos de Módulo: obrigatórios para cada módulo
- Branches Git: obrigatórias por módulo
- Ativação completa da squad obrigatória

Se o modo não estiver declarado: pergunte ao Diretor antes de prosseguir.

---

## Subagentes vs Janelas Separadas

**Janela separada** → agente precisa de memória entre sessões (Desenvolvedor, Auditor, Orquestrador, QA)
**Subagente** → tarefa paralela dentro de uma sessão, sem necessidade de memória (pesquisa no /plan, auditoria paralela de arquivos, atualização de STATUS.md)

Na dúvida: janela separada. Subagentes são uma otimização, não um padrão.

---

## SPEC.md e ARCH.md — Projetos Novos vs Existentes

### Projeto novo (começa do zero)
Crie SPEC.md e ARCH.md como documentos completos antes de qualquer código ser escrito.
Siga as Fases 3 e 5 do framework buildflow.

### Projeto existente (já tem documentação)
NÃO crie documentos duplicados. Crie wrappers enxutos (~100 linhas cada):

```
SPEC.md (wrapper) — índice + gate
- O que é este produto (2-3 linhas)
- Links para documentos de spec existentes
- O que está FORA do escopo
- Critérios de qualidade
- Gate: Diretor aprova antes de qualquer módulo começar

ARCH.md (wrapper) — índice + gate
- Stack definida (1 linha cada)
- Links para documentos técnicos existentes
- Lista de módulos na ordem de execução
- Gate: Diretor aprova antes de qualquer código ser escrito
```

O wrapper funciona como gate — não como duplicata.
Se SPEC.md e ARCH.md wrappers não existem: crie antes de começar.
Se já existem: verifique se estão aprovados antes de prosseguir.

---

## A Squad de Desenvolvimento — Claude Code

Cada agente roda em uma janela separada do VS Code.
Cada janela aponta para a pasta do projeto.
Cada agente tem seu próprio CLAUDE.md, MEMORY.md e DECISIONS.md.

### Squad Escalável — escolha pela complexidade do módulo

**Módulo simples** — segue template existente, sem novas integrações:
```
Orquestrador + Desenvolvedor + Auditor de Código
QA e Segurança rodam uma vez antes do lançamento — não por módulo
```

**Módulo complexo** — nova arquitetura, integração externa, infra, auth, design system:
```
Squad completa: Orquestrador + Arquiteto + Desenvolvedor + Auditor + QA Tester + Revisor de Segurança
QA e Segurança rodam por módulo
```

**Como classificar um módulo:**
- Simples: calculadora, página de conteúdo, formulário seguindo padrão existente
- Complexo: autenticação, pagamento, novo schema de banco, integração de API, infraestrutura

O Orquestrador classifica cada módulo antes de ativar a squad.

### Referência da Squad Completa

| Agente | Papel | Quando ativar |
|--------|-------|---------------|
| Orquestrador | Coordena squad, mantém STATUS.md | Sempre ativo |
| Arquiteto | ARCH.md + planos de módulo | Módulos complexos + Fase 0 |
| Desenvolvedor | Escreve código usando writers especializados | Todos os módulos |
| Auditor de Código | Revisa toda entrega do Desenvolvedor | Após toda entrega |
| QA Tester | Testa o que foi construído | Módulos complexos + antes do lançamento |
| Revisor de Segurança | Verifica vulnerabilidades | Módulos complexos + antes do lançamento |

### Regras para a squad de desenvolvimento

- Nenhum agente escreve código antes de SPEC.md e ARCH.md serem aprovados
- Nenhum agente escreve código antes do plano do módulo ser aprovado
- Nenhuma feature vai para QA antes de passar pelo Auditor de Código
- Nenhum código vai para produção antes do Revisor de Segurança aprovar
- Todo agente lê SPEC.md e ARCH.md antes de começar
- Todo agente segue as regras do PT-BUILDFLOW-GLOBAL.md

---

## Fases de Desenvolvimento

### Fase 0 — Arquitetura (agente Arquiteto)

O Arquiteto lê SPEC.md e entrega ARCH.md:

```
ARCH.md contendo:
- Estrutura de pastas e arquivos
- Schema do banco de dados (tabelas, campos, relacionamentos)
- Contratos de API (endpoints, inputs, outputs)
- Mapa de componentes (o que se conecta ao quê)
- Variáveis de ambiente necessárias
- Integrações de terceiros e como se conectam
- Lista de módulos na ordem de execução com dependências
```

Regras:
- Nenhum código é escrito nesta fase — apenas estrutura
- Diretor aprova ARCH.md antes da Fase 1 iniciar
- Se ARCH.md mudar durante o desenvolvimento, todos os agentes são notificados

Briefing para o Arquiteto:
```
Leia SPEC.md e PT-BUILDFLOW-GLOBAL.md.
Sua missão: definir a arquitetura completa para este produto.
NÃO escreva código. Defina apenas estrutura.
Toda decisão deve ser justificada pelos requisitos do SPEC.md.
Entregue ARCH.md. Aguarde aprovação do Diretor antes de qualquer construção.
```

---

### Fase 1 — Planejamento do Módulo (agente Arquiteto, antes de cada módulo)

Antes do Desenvolvedor tocar qualquer módulo, o Arquiteto roda o /plan.

A fase /plan faz duas coisas:
1. Pesquisa DENTRO do projeto por código existente para reutilizar
2. Pesquisa FORA do projeto por padrões documentados e boas práticas

O Arquiteto entrega um Plano do Módulo contendo:

```
PLANO DO MÓDULO — [nome do módulo]
Branch: feature/[nome-do-modulo]

Visão geral: [o que este módulo faz em uma frase]

Arquivos a CRIAR:
- [caminho exato] — [o que contém]
- [caminho exato] — [o que contém]

Arquivos a MODIFICAR:
- [caminho exato] — [o que muda e por quê]

Arquivos a REUTILIZAR (já existem):
- [caminho exato] — [como será usado]

Comportamentos:
- Caminho feliz: [o que acontece quando tudo funciona]
- Edge cases: [o que acontece nos limites]
- Estados de erro: [o que acontece quando falha]

Mudanças no banco de dados (se houver):
- [tabela] — [o que muda]

Dependências externas (se houver):
- [serviço/API] — [como é usado]

Agentes writers necessários:
- [tipo de writer] — [quais arquivos]
```

Regras:
- Diretor aprova o Plano do Módulo antes do Desenvolvedor iniciar
- Se um arquivo não está no plano, o Desenvolvedor não o toca
- Esta é a regra mais importante para prevenir "IA desobediente"

---

### Fase 2 — Construção (agente Desenvolvedor)

O Desenvolvedor constrói um módulo por vez usando o Plano do Módulo.
Nunca constrói além do que o plano especifica.

#### Agentes Writers Especializados

O Desenvolvedor usa writers especializados por tipo de arquivo.
Cada writer tem suas próprias regras e padrões:

| Writer | Responsabilidade |
|--------|-----------------|
| component-writer | Elementos visuais — botões, formulários, cards, layouts |
| action-writer | Lógica server-side — processa ações do usuário, salva dados |
| hook-writer | Conecta UI às ações do servidor — o "fio" entre eles |
| integration-writer | Serviços externos — email, pagamentos, APIs |
| model-writer | Estrutura do banco de dados — tabelas, schemas, relacionamentos |
| route-writer | Endpoints de API — comunicação entre frontend e backend |
| test-writer | Testes automatizados — unitários, integração, e2e |

Regras para cada writer:
- Toca apenas arquivos listados no Plano do Módulo
- Pesquisa componentes existentes antes de criar novos
- Nunca duplica código que já existe no projeto
- Sempre segue os padrões do ARCH.md — nunca inventa novos

Briefing para o Desenvolvedor:
```
Leia SPEC.md, ARCH.md, o Plano do Módulo e PT-BUILDFLOW-GLOBAL.md.
Sua missão: construir [nome do módulo] exatamente como especificado no Plano do Módulo.
Use o agente writer apropriado para cada tipo de arquivo.
Toque apenas arquivos listados no Plano do Módulo.
Antes de criar qualquer coisa: pesquise o projeto por código existente para reutilizar.
Siga os padrões do ARCH.md exatamente. Se precisar desviar, pare e sinalize.
Após concluir: entregue um resumo do que foi construído para o Auditor de Código.
```

---

### Fase 3 — Auditoria (agente Auditor de Código)

O Auditor de Código revisa todo módulo que o Desenvolvedor entrega.
Isso não é opcional. Toda entrega passa pela auditoria.

O que o Auditor verifica:
- O código faz o que o SPEC.md requer
- Segue a estrutura do ARCH.md
- Corresponde ao Plano do Módulo arquivo por arquivo — sem arquivos extras, sem faltantes
- Há código duplicado que já existia no projeto
- Há bugs óbvios ou edge cases não tratados
- Há valores hardcoded que deveriam ser variáveis de ambiente
- O tratamento de erros está presente e é significativo
- O código é legível por um agente futuro

Formato do relatório de auditoria:
```
# AUDITORIA DE CÓDIGO — [nome do módulo]
# Data: [data]

## VEREDICTO: APROVADO / PRECISA DE REVISÃO

## Arquivos verificados vs Plano do Módulo
- [arquivo] — no plano: sim/não — criado/modificado: sim/não

## Problemas encontrados
### Críticos (corrigir antes do QA):
- [problema + localização + correção sugerida]

### Importantes (corrigir antes da produção):
- [problema + localização + correção sugerida]

### Menores (nice to have):
- [problema + localização + correção sugerida]

## O que o Desenvolvedor fez bem
[pelo menos um ponto positivo — previne super-correção]
```

Briefing para o Auditor de Código:
```
Leia SPEC.md, ARCH.md, o Plano do Módulo e PT-BUILDFLOW-GLOBAL.md.
Sua missão: auditar [nome do módulo] entregue pelo Desenvolvedor.
Cruze cada arquivo com o Plano do Módulo.
Sinalize qualquer arquivo tocado que não estava no plano.
Sinalize qualquer código duplicado encontrado no projeto.
Seu veredicto (APROVADO / PRECISA DE REVISÃO) libera o QA.
Nada vai para QA sem sua aprovação.
```

---

### Fase 4 — Testes (agente QA Tester)

O QA Tester testa o que o Auditor aprovou.

O que o Tester verifica:
- Funciona conforme descrito no SPEC.md (caminho feliz)
- O que acontece nos limites (campos vazios, tamanho máximo, input inválido)
- O que acontece quando integrações falham (API fora, timeout do banco)
- Funciona no mobile (se aplicável)
- Funciona em diferentes navegadores (se aplicável)
- Mensagens de erro são claras e úteis ao usuário

Formato do relatório de testes:
```
# RELATÓRIO DE QA — [nome do módulo]
# Data: [data]

## VEREDICTO: PASSOU / FALHOU

## Testes realizados
| Teste | Esperado | Resultado | Status |
|-------|----------|-----------|--------|
| [teste] | [esperado] | [real] | ✅/❌ |

## Bugs encontrados
### Bloqueadores (corrigir antes do merge):
- [bug + passos para reproduzir + comportamento esperado]

### Não-bloqueadores (corrigir antes da produção):
- [bug + passos para reproduzir + comportamento esperado]
```

Briefing para o QA Tester:
```
Leia SPEC.md e PT-BUILDFLOW-GLOBAL.md.
Sua missão: testar [nome do módulo] que passou pela Auditoria de Código.
Teste o caminho feliz primeiro. Depois quebre.
Todo bug precisa: o que você fez, o que aconteceu, o que deveria ter acontecido.
Seu veredicto (PASSOU / FALHOU) libera o merge para main.
```

---

### Fase 5 — Revisão de Segurança (agente Revisor de Segurança)

Roda uma vez — antes do produto ir para produção.
Não após cada módulo — apenas no final.

O que o Revisor de Segurança verifica:
- Chaves de API e secrets estão em variáveis de ambiente (nunca no código)
- Input do usuário é validado e sanitizado
- Queries de banco estão protegidas contra injeção
- Autenticação foi implementada corretamente
- Rotas sensíveis estão protegidas
- Lógica de negócio está no servidor, nunca no cliente
- Mensagens de erro são seguras (não expõem detalhes internos)
- Dependências estão atualizadas e sem vulnerabilidades conhecidas

Formato do relatório de segurança:
```
# RELATÓRIO DE SEGURANÇA
# Data: [data]
# Status: LIBERADO PARA PRODUÇÃO / BLOQUEADO

## Problemas críticos (bloqueiam produção):
- [problema + risco + correção]

## Problemas importantes (corrigir em 30 dias):
- [problema + risco + correção]

## Recomendações:
- [boa prática ainda não implementada]
```

---

## Disciplina de Git

### Branch por módulo — não por dia, não por sessão

Todo módulo recebe sua própria branch antes do Desenvolvedor escrever uma linha.

```bash
git checkout main
git pull origin main
git checkout -b feature/[nome-do-modulo]
```

O trabalho acontece na branch. Quando o QA passa:

```bash
git checkout main
git merge feature/[nome-do-modulo]
git push origin main
git branch -d feature/[nome-do-modulo]
```

Diretor aprova o merge. Orquestrador executa.
Nada faz merge para main sem aprovação do QA.

### Formato de commit — dentro da branch

```
feat: [nome do módulo] — [uma linha do que foi construído]
fix: [nome do módulo] — [uma linha do que foi corrigido]
```

### Por que branches importam

Se um módulo quebrar, você reverte a branch — não o projeto inteiro.
Main sempre contém código funcionando e aprovado.
Você pode mostrar o produto a qualquer momento sem medo.

---

## Gerenciamento de Contexto

O Claude Code perde foco quando o contexto enche.
Sintomas: contradizer decisões anteriores, padrões inconsistentes,
ignorar instruções do CLAUDE.md, tocar arquivos que não estão no plano.

Regras:
- Rode /compact quando o contexto atingir 50%
- Rode /clear quando mudar para um módulo completamente diferente
- Nunca misture planejamento e execução na mesma sessão
- Se o agente começar a contradizer o ARCH.md: inicie uma nova sessão
  com SPEC.md, ARCH.md, Plano do Módulo e CLAUDE.md re-ancorados
- Se o contexto degradar: é mais barato reiniciar do que corrigir a bagunça

---

## Quality Gates — Nada Passa Sem Estes

| Gate | Quem aprova | O que bloqueia |
|------|------------|----------------|
| SPEC.md aprovado | Diretor | Nada é construído |
| ARCH.md aprovado | Diretor | Nenhum código é escrito |
| Plano do Módulo aprovado | Diretor | Desenvolvedor não começa |
| Módulo auditado | Auditor de Código | Módulo não vai para QA |
| Módulo testado | QA Tester | Módulo não faz merge |
| Segurança liberada | Revisor de Segurança | Nada vai para produção |

---

## O Padrão que se Aplica a Todo Projeto

Uma entrega é aprovada quando:
- Faz exatamente o que o SPEC.md descreve
- Segue a estrutura do ARCH.md
- Corresponde ao Plano do Módulo arquivo por arquivo
- Passa pela Auditoria de Código
- Passa pelo QA
- Não tem problemas críticos de segurança

Uma entrega é rejeitada quando:
- Faz algo que o SPEC.md não especificou
- Contradiz o ARCH.md
- Toca arquivos que não estavam no Plano do Módulo
- Duplica código que já existia
- Tem bugs críticos
- Foi construída sem um Plano do Módulo

A pergunta antes de todo lançamento:
**"Se isso falhar, eu me sentiria confortável explicando por que enviamos mesmo assim?"**
Se a resposta for não — não envie.

---

## Radar de Eficiência — Edição Dev

Ao final de toda sessão, verifique:

| Detectado | Ação |
|-----------|------|
| Mesmo tipo de módulo construído duas vezes | Crie um template reutilizável |
| Mesmo bug encontrado em múltiplos módulos | Adicione regra ao briefing do Auditor |
| Mesmo teste de QA repetido em módulos | Crie um checklist de testes |
| Mesma pergunta do ARCH.md feita duas vezes | Atualize o ARCH.md com a resposta |
| Agente tocando arquivos que não estão no plano | Reforce a disciplina do Plano do Módulo |
| Agente duplicando código existente | Adicione regra de busca-primeiro ao briefing do Desenvolvedor |
| Agente ignorando SPEC.md | SPEC.md está longo demais — divida por módulo |

---

## Encerramento de Sessão — Edição Dev

Antes de encerrar qualquer sessão de desenvolvimento:

```
□ Módulo atual: APROVADO pelo Auditor / PASSOU no QA / ou claramente marcado como EM PROGRESSO
□ Branch commitada (se módulo completo — merge para main após QA)
□ MEMORY.md atualizado com o que foi construído
□ DECISIONS.md atualizado com decisões arquiteturais tomadas
□ STATUS.md atualizado
□ Próximo módulo claramente definido no MEMORY.md
□ Questões abertas escaladas ao Diretor
```

---

## Erros Comuns — Aprenda com Projetos Reais

**Erro 1 — Começar a codar antes da arquitetura ser definida**
O Desenvolvedor constrói algo, o Arquiteto chega e diz que a estrutura está errada.
Tudo é reescrito.
Solução: Arquiteto sempre vai primeiro. ARCH.md antes de qualquer código.

**Erro 2 — Pular o Plano do Módulo**
O Desenvolvedor toca arquivos que não deveriam mudar.
Uma coisa quebra outra. O problema do "cobertor curto".
Solução: Plano do Módulo é obrigatório. Todo módulo. Sem exceções.

**Erro 3 — Construir o produto inteiro em uma sessão**
O contexto enche, o agente perde foco, inconsistências aparecem.
Solução: Um módulo por sessão. Branch. Auditoria. Teste. Merge.

**Erro 4 — Não pesquisar código existente antes de escrever**
O Desenvolvedor cria um componente de botão que já existe.
Agora tem dois. Depois três. A manutenção fica impossível.
Solução: busca-primeiro faz parte de todo briefing do Desenvolvedor.

**Erro 5 — Pular a Auditoria de Código porque "parece certo"**
45% do código gerado por IA contém vulnerabilidades.
"Parece certo" não é um padrão de qualidade.
Solução: Auditoria de Código é obrigatória. Sem exceções.

**Erro 6 — Testar apenas o caminho feliz**
O produto funciona perfeitamente em demos e quebra com usuários reais.
Solução: QA Tester testa explicitamente edge cases e cenários de falha.

**Erro 7 — Ir para produção sem revisão de segurança**
Lógica de negócio no frontend. Chaves de API no código.
Qualquer pessoa com as ferramentas de desenvolvedor do navegador pode explorar isso.
Solução: Revisor de Segurança roda uma vez antes de todo deploy em produção.

**Erro 8 — Fazer merge direto para main sem branch**
Algo quebra e afeta tudo que estava funcionando.
Solução: Branch por módulo. Main sempre limpo e funcionando.

---

Licença MIT · Copyright (c) 2026 Caio George Santos
