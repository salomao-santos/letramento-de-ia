---
title: "Sanity Checks para Codebases"
type: concept
tags: [qualidade, ci, automação, harness-engineering, sensores]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[wiki/sources/engenharia-era-piloto-automatico]]"]
---

# Sanity Checks para Codebases

## Conceito

"Cheque de sanidade" — verificação automatizada que avalia se uma mudança mantém o codebase sadio antes de ir para produção. Evolução do Sonar para a era de IA: agora pode-se inspecionar o codebase inteiro porque ficou mais barato.

## Características

- Roda no CI, antes do deploy
- Pode usar **multimodelos/multiagentes** para validação cruzada (interseção de outputs)
- Verifica compliance com decisões de arquitetura e code guidelines
- Cada empresa define suas próprias convenções

## Feed Forward vs Feedback

([[wiki/entities/martin-fowler]])

- **Feed forward (context engineering):** importante mas é apenas o começo da conversa
- **Feedback (sanity check):** mais crucial — garante que o código produzido está compliant com o que foi definido

> "Quanto mais perto da produção, mais custoso é o software do ponto de vista de manutenção. Quanto antes antecipar, melhor."

## Na prática

| Abordagem | Ferramenta/Técnica |
|-----------|-------------------|
| Determinística | Linters, type checkers, ArchUnit, dependency-cruiser, fitness functions |
| Probabilística | LLM-as-judge, multimodelo para consensus |
| Híbrida | Checagem determinística quando possível + LLM para o restante |

## Pré-mortem como complemento

Antes de subir feature nova:
1. Gerar cenários de pré-mortem (o que pode dar errado?)
2. Criar testes para esses cenários
3. Deploy com canário (1%) + feature flag
4. Rodar cenários de pré-mortem no canário
5. Qualidade intencional e proativa a cada deploy

## Relação com sensores

Sanity checks são uma aplicação do conceito de [[wiki/concepts/sensores-computacionais]] na camada de CI/CD, com a adição de sensores inferenciais (LLM) para cobrir aspectos que checks determinísticos não alcançam.

## Ver também

- [[wiki/concepts/sensores-computacionais]]
- [[wiki/concepts/harness-engineering]]
- [[wiki/concepts/tdd-como-especificacao]]
- [[wiki/sources/engenharia-era-piloto-automatico]]
