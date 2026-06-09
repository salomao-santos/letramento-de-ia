---
title: "O teste que você não escreveu virou o bug que o agente escondeu"
type: source
tags: [tdd, testes, mutation-testing, property-based-testing, coding-com-ia]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[raw/clippings/O teste que você não escreveu virou o bug que o agente escondeu]]"]
author: "Zarathon Viana"
published: 2026-05-14
---

# TDD na era dos agentes

## Resumo

Terceiro artigo da série. Defende que TDD deixou de ser dogma e virou a ferramenta mais pragmática de controle sobre agentes de coding. O teste não é mais verificação — é especificação. O custo de escrever código caiu pra quase zero; o que ficou caro foi especificar a intenção.

## Tese Central

> "Na era dos agentes, não ter teste é o cenário mais caro e mais demorado que existe."

## Conceitos-chave

### Teste como especificação (não verificação)
- Define comportamento esperado em linguagem determinística
- Cria sensor computacional (barato, provado, determinístico)
- Define limites do que o agente pode fazer

### Red-Green-Refactor com agente
- **Red: humano** — escreve o teste que falha (não delegar!)
- **Green: agente** — implementa código mínimo pra passar
- **Refactor: colaboração** — agente propõe, humano valida

### Vertical slicing vs Horizontal slicing
- Horizontal (anti-padrão): todos os testes primeiro, depois toda implementação
- Vertical (correto): um teste → implementação → próximo teste

### Teatro de coverage
- 92% coverage pode ser mentira se testes foram escritos DEPOIS do código
- "Espelho autorreferente": agente testa o que ele mesmo fez, inclusive confirmando bugs

### Mutation testing
- Introduz mutações no código e verifica se testes detectam
- 100% coverage + 4% mutation score = 96% dos bugs passam

### Property-based testing (PBT)
- Define propriedades universais, não exemplos específicos
- Gera centenas/milhares de inputs aleatórios
- "O LLM não adivinha invariante"
- Anthropic publicou pesquisa no NeurIPS 2025 sobre agente que escreve PBT

### Kent Beck e augmented coding
- Beck usa TDD estrito com agentes (projeto BPlusTree3)
- "Vibe coding" ≠ "Augmented coding" — o segundo mantém padrões de engenharia
- O agente tentou deletar teste falhando; Beck impediu

## Frameworks que convergem para TDD
- **Superpowers** (Jesse Vincent): 650k+ installs, TDD ortodoxo obrigatório
- **BMAD**: TDD como prática recomendada
- **GSD**: Plan-Execute-Verify com teste como base
- **Compound Engineering**: 80% planejamento/revisão, 20% execução

## Dados-chave
- GitClear: code churn quase dobrou no período de adoção de IA (211M linhas analisadas)
- Qodo: 65% dos devs reportam lacunas de contexto como principal fonte de baixa qualidade
- DORA 2025: instabilidade de entrega continua subindo desde adoção de IA generativa

## Conceitos Relacionados
- [[wiki/concepts/tres-camadas-coding-ia]]
- [[wiki/concepts/sensores-computacionais]]
- [[wiki/concepts/tdd-como-especificacao]]
- [[wiki/concepts/mutation-testing]]
- [[wiki/concepts/property-based-testing]]

## Referências
- Kent Beck BPlusTree3: system prompt com TDD obrigatório
- Matt Pocock Skills: https://github.com/mattpocock/skills
- Superpowers: https://github.com/obra/superpowers
- Fowler & Böckeler (2026): https://martinfowler.com/articles/harness-engineering.html
