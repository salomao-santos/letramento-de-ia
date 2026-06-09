---
title: "Spec-Driven Development"
type: concept
tags: [spec-driven-development, workflows, especificação]
created: 2026-06-08
updated: 2026-06-09
sources: ["[[wiki/sources/spec-driven-development]]", "[[wiki/sources/software-fundamentals-matter-more-than-ever]]", "[[wiki/sources/full-walkthrough-workflow-ai-coding]]", "[[wiki/sources/spec-driven-limite-harness-proximo-passo]]", "[[wiki/sources/spec-driven-guia-completo-waldemar]]", "[[wiki/sources/fluxo-completo-dev-avancado-ia]]"]
---

# Spec-Driven Development (SDD)

## Definição

Abordagem que propõe escrever uma "spec" (especificação) antes de escrever código com IA. A spec se torna fonte da verdade compartilhada entre humano e IA.

## Três Níveis

| Nível | Criação | Manutenção | Exemplo |
|-------|---------|-----------|---------|
| Spec-first | Spec → código | Spec descartada | Kiro, spec-kit |
| Spec-anchored | Spec → código | Spec mantida e editada | Tessl (aspiração) |
| Spec-as-source | Spec = artefato principal | Humano nunca edita código | Tessl (exploratório) |

## O que é uma spec?

Artefato estruturado, orientado a comportamento, escrito em linguagem natural, que expressa funcionalidade e serve como guia para agentes de coding.

Diferente de **memory bank** (contexto geral para todas as sessões):
- Memory bank: AGENTS.md, product.md, architecture.md
- Specs: específicas para uma feature/task

## Ferramentas

- [[wiki/entities/kiro-ide]] — Requirements → Design → Tasks
- **spec-kit** (GitHub) — Constitution → Specify → Plan → Tasks
- **Tessl** — Spec ↔ Code (mapeamento 1:1, bidirecional)

## Críticas (Böckeler)

1. **Tamanho do problema:** workflows one-size-fits-all não funcionam para todas as escalas
2. **Review overload:** muitos markdown files para revisar pode ser pior que revisar código
3. **Falsa sensação de controle:** agente frequentemente ignora partes da spec
4. **Separação funcional/técnica:** difícil na prática
5. **Paralelo com MDD:** risco de herdar desvantagens (inflexibilidade + não-determinismo)

## Crítica prática (Matt Pocock)

[[wiki/entities/matt-pocock|Matt Pocock]] testou o ciclo "spec → code → ignore code → edit spec → regenerate" e constatou degradação progressiva: a cada iteração, o código ficava pior. Conclusão: specs-to-code é "vibe coding por outro nome" quando não se investe no design do sistema.

A entropia de software (Pragmatic Programmer) se aplica: sem investimento consciente no design a cada mudança, o sistema se degrada inevitavelmente. A spec sozinha não impede isso.

No workshop prático, Matt reforça: "This is not specs to code. This is not where we're ignoring the code. We actually keep the code in mind throughout the whole process." A alternativa é:
- Usar grill session para **alinhamento** (não para gerar artefato)
- PRD como documento de destino descartável (doc rot se mantido)
- Manter mapa mental dos módulos durante todo o planejamento
- Feedback loops (TDD, types) como validação real, não a spec

## Valor real

O princípio de **spec-first** (pensar e estruturar antes de pedir ao agente) é valioso. As ferramentas e workflows elaborados ainda estão em maturação.

## Operacionalização prática (Waldemar Neto — Guia Completo)

[[wiki/sources/spec-driven-guia-completo-waldemar]] demonstra o workflow completo usando a skill **TLC Spec Driven**:

### RPI — Research, Plan, Implement

1. **Research:** janela dedicada para explorar codebase, MCPs, docs — descobrir o que precisa fazer
2. **Plan:** salvar em Markdown (spec + design + tasks) — preserva conhecimento sem tokens futuros
3. **Implement:** janela NOVA e limpa, executando tasks com referência apenas aos markdowns

### Subagents para escala

- Na fase de implement, o agente principal delega tasks paralelas a subagents
- Caso real: 90 arquivos modificados, 4 subagents simultâneos, janela principal em 50K tokens
- Cada subagent tem contexto próprio — menos chance de erro

### Estado como continuidade

Arquivo state que guarda decisões tomadas durante implementação. Permite:
- Retomar em nova sessão ("continua o projeto X")
- Separar entrega em múltiplos PRs
- Rastreabilidade de decisões do agente

### Demonstração end-to-end (vídeo prático)

[[wiki/sources/fluxo-completo-dev-avancado-ia]] é a demonstração prática do RPI num case real (integração Stripe em monorepo):

1. Design doc no Confluence → IA avalia completude do MVP
2. IA quebra em tasks granulares (não tasks micro) → cria no Jira via skill
3. IA avalia paralelização (identifica dependências)
4. Novo contexto → plano com modelo caro (Sonnet) → execução em agente separado com modelo barato (Composer)
5. Worktrees do Git para paralelizar tasks independentes (2-3 agentes simultâneos)
6. Revisão humana entre cada ciclo

Meta operacional: **≤30% de 200K tokens** por janela. A 44%, "ela vai começar a alucinar".

### Regra de ouro

> Manter janela de contexto ≤ 200K tokens. Quanto maior, mais alucinação. Separar research de implement em janelas diferentes.

## Limitações explícitas (Waldemar Neto)

[[wiki/sources/spec-driven-limite-harness-proximo-passo]] categoriza 6 falhas de agentes e mostra que spec driven resolve apenas 2 completamente:

| Falha | Spec resolve? |
|-------|--------------|
| One Shot Hero (tudo de uma vez) | ✅ Quebra em tasks |
| Vitória prematura ("terminei") | ✅ Define "done" explícito |
| Amnésia entre sessões | ❌ Não guarda estado |
| Validação superficial (curl 200 = pronto) | ❌ Nem todo framework enforça testes |
| Self-judge (mesmo agente julga) | ❌ Spec é single-process |
| Slope acumulado (5% pior a cada task) | ❌ Não enforça qualidade contínua |

Conclusão: spec-driven é **feed forward puro** — diz o que fazer, mas não verifica se foi feito certo. Para sistemas inteiros, precisa de harness completo (feedback + memória + multi-agente).

## Relação com outros conceitos

- Specs são uma forma de **guide (feedforward)** no modelo de [[wiki/concepts/harness-engineering]]
- TDD ([[wiki/concepts/tdd-como-especificacao]]) é uma alternativa/complemento determinístico: teste como spec executável

## Ver também

- [[wiki/sources/spec-driven-development]]
- [[wiki/sources/software-fundamentals-matter-more-than-ever]]
- [[wiki/sources/spec-driven-limite-harness-proximo-passo]]
- [[wiki/sources/spec-driven-guia-completo-waldemar]]
- [[wiki/sources/fluxo-completo-dev-avancado-ia]]
- [[wiki/concepts/harness-engineering]]
- [[wiki/concepts/tdd-como-especificacao]]
- [[wiki/concepts/compaction-de-contexto]]
