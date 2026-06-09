---
title: "Spec-Driven Development"
type: concept
tags: [spec-driven-development, workflows, especificação]
created: 2026-06-08
updated: 2026-06-09
sources: ["[[wiki/sources/spec-driven-development]]", "[[wiki/sources/software-fundamentals-matter-more-than-ever]]"]
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

## Valor real

O princípio de **spec-first** (pensar e estruturar antes de pedir ao agente) é valioso. As ferramentas e workflows elaborados ainda estão em maturação.

## Relação com outros conceitos

- Specs são uma forma de **guide (feedforward)** no modelo de [[wiki/concepts/harness-engineering]]
- TDD ([[wiki/concepts/tdd-como-especificacao]]) é uma alternativa/complemento determinístico: teste como spec executável

## Ver também

- [[wiki/sources/spec-driven-development]]
- [[wiki/sources/software-fundamentals-matter-more-than-ever]]
- [[wiki/concepts/harness-engineering]]
- [[wiki/concepts/tdd-como-especificacao]]
