---
title: "Sensores Computacionais"
type: concept
tags: [determinismo, ci-cd, linter, testes, arquitetura]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[wiki/sources/as-3-camadas-do-coding-com-ia]]", "[[wiki/sources/arquitetura-na-era-dos-agentes]]", "[[wiki/sources/tdd-na-era-dos-agentes]]"]
---

# Sensores Computacionais

## Definição

Termo de [[wiki/entities/martin-fowler]] e Birgitta Böckeler (Thoughtworks). São verificações automatizadas que detectam problemas estruturais com **confiabilidade determinística**.

> "São baratos, provados e determinísticos. Exatamente o oposto do LLM. E por isso complementam ele tão bem."

## Características

- **Determinísticos:** passa ou não passa. Sem "mais ou menos".
- **Baratos:** rodam em segundos no CI.
- **Confiáveis:** não alucinam, não inventam, não cansam.

## Exemplos

| Tipo | Ferramenta | O que detecta |
|------|-----------|---------------|
| Lint/Estilo | ESLint, Ruff, Prettier | Violações de estilo e padrão |
| Type checking | TypeScript strict, mypy | Tipos incorretos |
| Análise estática | SonarQube, CodeQL, Semgrep | Complexidade, segurança |
| Testes de arquitetura | [[wiki/entities/archunit]], [[wiki/entities/dependency-cruiser]] | Drift arquitetural |
| Testes unitários | JUnit, pytest, Jest | Comportamento incorreto |
| Mutation testing | PIT, Stryker | Fraqueza da suíte de testes |
| Coverage gates | CI/CD | Regressão de cobertura |

## Papel na era dos agentes

O modelo é probabilístico. Os sensores são determinísticos. Juntos formam um sistema de cercas:

- O agente gera código (probabilístico)
- O sensor verifica (determinístico)
- Se falhou, o agente recebe a mensagem de erro e corrige

Fowler chama o feedback do sensor ao agente de "positive prompt injection" — injeção de contexto que direciona pro caminho certo.

## Regra de ouro

> Rode como **teste** (quebra o build), não como **lint** (só avisa). Na era dos agentes, aviso não basta. Tem que travar.

## Ver também

- [[wiki/concepts/tres-camadas-coding-ia]]
- [[wiki/concepts/harness-engineering]]
