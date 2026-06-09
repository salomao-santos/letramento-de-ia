---
title: "Mutation Testing (Teste de Mutação)"
type: concept
tags: [testes, qualidade, mutation-testing]
created: 2026-06-08
updated: 2026-06-09
sources: ["[[wiki/sources/tdd-na-era-dos-agentes]]", "[[wiki/sources/harness-beyond-skills-sensors]]"]
---

# Mutation Testing (Teste de Mutação)

## O que é

Técnica que introduz pequenas mutações no código (troca `>` por `>=`, `+` por `-`, `true` por `false`) e verifica se os testes detectam. Se os testes continuam passando após a mutação, eles são **fracos**.

## Por que importa na era IA

É o **detector de mentira** para suítes de teste. Mata a ilusão do coverage bonito.

> "Uma suite com 100% de coverage mas 4% de mutation score executa toda linha e deixa passar 96% dos bugs potenciais."

## Ferramentas

| Linguagem | Ferramenta |
|-----------|-----------|
| Java | PIT (pitest) |
| JavaScript/TypeScript | Stryker |
| Python | mutmut, cosmic-ray |

## Fluxo com agente

1. Agente gera código e testes
2. Mutation testing roda nos testes
3. Mutantes sobreviventes expõem fraquezas
4. Agente melhora os testes para matar mutantes

## Quando usar

- Após o agente gerar testes (especialmente se gerou depois do código)
- Em fluxos de negócio críticos
- Como gate no CI para módulos sensíveis

## Limitação prática: custo computacional

Böckeler confirma em [[wiki/sources/harness-beyond-skills-sensors]]: mutation testing é **resource intensive** (muda código → roda testes → repete). Não cabe como sensor contínuo em tempo real. Soluções:

- **Modo incremental** (Stryker): testa apenas mutantes em código alterado
- **Runs manuais periódicos** (drift detection)
- **Resultados em JSON** → script customizado para queries + IA analisa hotspots

## Caso real: coverage alta ≠ proteção

Arquivo com 100% statement coverage e 75% branch coverage → 13 mutantes sobreviventes. Causa: cobertura vinha de acceptance test que chamava o módulo mas **não assertava valores internos**. Mutation testing revelou o gap que coverage escondeu.

## Ver também

- [[wiki/concepts/tdd-como-especificacao]]
- [[wiki/concepts/property-based-testing]]
- [[wiki/concepts/sensores-computacionais]]
- [[wiki/sources/harness-beyond-skills-sensors]]
- [[wiki/sources/maintainability-sensors]]
