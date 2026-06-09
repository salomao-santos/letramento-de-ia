---
title: "Software Fundamentals Matter More Than Ever"
type: source
tags: [fundamentos, arquitetura, tdd, deep-modules, design-concept, ubiquitous-language, matt-pocock]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[raw/clippings/Software Fundamentals Matter More Than Ever — Matt Pocock]]"]
---

# Software Fundamentals Matter More Than Ever — Matt Pocock

## Metadados

- **Autor:** [[wiki/entities/matt-pocock|Matt Pocock]]
- **Tipo:** Palestra (conferência)
- **Data:** 2025-06-08
- **URL:** https://www.youtube.com/watch?v=v4F1gFy-hqg
- **Duração:** ~18 min

## Tese central

> Código não é barato. Código ruim é mais caro do que jamais foi.

Fundamentos de engenharia de software importam **mais** na era da IA, não menos. Um codebase bem desenhado amplifica o ganho com IA; um codebase ruim impede que se colha qualquer benefício.

## Crítica a specs-to-code

Matt testou o workflow "specs-to-code" (escrever spec → gerar código → ignorar o código → editar a spec → regenerar) e constatou que a cada iteração o código ficava pior. Chama isso de "vibe coding por outro nome". A entropia do software (conceito do Pragmatic Programmer) se aplica: sem investimento consciente no design, o sistema se degrada a cada mudança.

## Failure modes e soluções (5 skills)

### 1. "A IA não fez o que eu queria" — Design Concept (Frederick Brooks)

**Problema:** humano e IA não compartilham a mesma visão do que está sendo construído.

**Solução:** "Grill Me" — skill que força a IA a interrogar o humano exaustivamente (40-100 perguntas) até atingir um *shared design concept*. Só então se gera um PRD ou issues.

> "Me entreviste implacavelmente sobre cada aspecto deste plano até que alcancemos um entendimento compartilhado."

### 2. "A IA é verbosa demais" — Ubiquitous Language (DDD)

**Problema:** humano e IA falam idiomas diferentes; a IA usa termos imprecisos ou genéricos.

**Solução:** criar um arquivo markdown de **linguagem ubíqua** — lista de termos com definições alinhadas, usados consistentemente no código, nas conversas e no planejamento. A IA pensa de forma menos verbosa e a implementação fica mais fiel ao plano.

Relação direta com [[wiki/concepts/llm-wiki-karpathy]]: o markdown de terminologia funciona como uma micro-wiki compartilhada.

### 3. "Funciona, mas não funciona" — TDD como freio de velocidade

**Problema:** a IA "outruns its headlights" — gera muito código antes de validar.

**Solução:** [[wiki/concepts/tdd-como-especificacao|TDD]] — força small steps. Teste primeiro (RED), IA implementa (GREEN), refatora (REFACTOR). A taxa de feedback é o limite de velocidade.

### 4. "A IA não entende meu codebase" — Deep Modules (Ousterhout)

**Problema:** codebases com shallow modules (muitos módulos pequenos com interfaces complexas) são difíceis de navegar para a IA.

**Solução:** reestruturar em **deep modules** — poucos módulos grandes, com interfaces simples que escondem complexidade interna. A IA navega melhor, os testes ficam mais fáceis (testa-se na interface), e o humano pode tratar os módulos como gray boxes.

### 5. "Meu cérebro não acompanha" — Design the interface, delegate the implementation

**Problema:** o humano se exaure tentando acompanhar tudo que a IA gera.

**Solução:** focar no design das interfaces dos deep modules. Delegar a implementação interna à IA. Testar pela interface. Isso reduz carga cognitiva sem perder controle.

## Livros referenciados

- *A Philosophy of Software Design* — John Ousterhout (deep modules, complexidade)
- *The Pragmatic Programmer* — Hunt & Thomas (entropia de software, outrunning headlights)
- *The Design of Design* — Frederick P. Brooks (design concept, design tree)
- *Domain-Driven Design* — Eric Evans (ubiquitous language)

## Citação-chave de Kent Beck

> "Invest in the design of the system every day."

Specs-to-code desinveste do design. A proposta de Matt é o oposto: investir constantemente no design, usando a IA como implementador tático sob direção estratégica do humano.

## Relação com outros conceitos da wiki

- [[wiki/concepts/spec-driven-development]] — crítica direta ao modelo "spec como compilador"
- [[wiki/concepts/tdd-como-especificacao]] — TDD como skill essencial para controlar a IA
- [[wiki/concepts/harness-engineering]] — ubiquitous language e design concept são formas de guide (feedforward)
- [[wiki/concepts/ambient-affordances]] — deep modules como affordance estrutural
- [[wiki/concepts/tres-camadas-coding-ia]] — alinhamento: fundamentos (camada 3) > ferramentas (camada 2)
- [[wiki/concepts/automation-complacency]] — "brain can't keep up" é sintoma de complacência com output da IA

## Referências

- [[raw/clippings/Software Fundamentals Matter More Than Ever — Matt Pocock]]
- GitHub: mattpocock/skills (13k+ stars)
- Curso: "Claude Code for Real Engineers"
