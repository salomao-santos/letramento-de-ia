---
title: "Mutation Testing"
type: concept
tags: [testes, qualidade, mutation-testing]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[wiki/sources/tdd-na-era-dos-agentes]]"]
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

## Ver também

- [[wiki/concepts/tdd-como-especificacao]]
- [[wiki/concepts/property-based-testing]]
- [[wiki/concepts/sensores-computacionais]]
