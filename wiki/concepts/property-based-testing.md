---
title: "Property-Based Testing"
type: concept
tags: [testes, pbt, alucinação, invariantes]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[wiki/sources/tdd-na-era-dos-agentes]]"]
---

# Property-Based Testing (PBT)

## O que é

Em vez de testar casos específicos ("se passo 100, retorna 10"), define **propriedades universais** que devem ser verdadeiras para qualquer input:

- "O desconto nunca é maior que o preço"
- "A soma das parcelas é igual ao total"
- "A lista ordenada tem o mesmo tamanho da original"

A biblioteca gera centenas/milhares de inputs aleatórios e verifica se a propriedade se mantém.

## Por que é a arma anti-alucinação

O LLM é bom em gerar código que satisfaz exemplos específicos. É péssimo em garantir propriedades universais. PBT pega exatamente os edge cases que ninguém (inclusive o LLM) pensou.

> "O LLM não adivinha invariante."

## Ferramentas

| Linguagem | Biblioteca |
|-----------|-----------|
| Python | Hypothesis |
| JavaScript | fast-check |
| Haskell | QuickCheck |
| Java | jqwik |

## Fluxo com agente

1. **Humano** define a propriedade/invariante
2. **Agente** gera os testes que verificam (pode usar Hypothesis, fast-check, etc.)
3. Biblioteca gera inputs aleatórios automaticamente
4. Falhas revelam edge cases não previstos

## Pesquisa da Anthropic

A Anthropic publicou no NeurIPS 2025 Deep Learning for Code Workshop uma pesquisa sobre agente que escreve PBTs autonomamente usando Hypothesis, lendo type annotations, docstrings e nomes de funções.

## Ver também

- [[wiki/concepts/mutation-testing]]
- [[wiki/concepts/tdd-como-especificacao]]
- [[wiki/concepts/sensores-computacionais]]
