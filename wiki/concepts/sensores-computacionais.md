---
title: "Sensores Computacionais"
type: concept
tags: [determinismo, ci-cd, linter, testes, arquitetura]
created: 2026-06-08
updated: 2026-06-09
sources: ["[[wiki/sources/as-3-camadas-do-coding-com-ia]]", "[[wiki/sources/arquitetura-na-era-dos-agentes]]", "[[wiki/sources/tdd-na-era-dos-agentes]]", "[[wiki/sources/harness-beyond-skills-sensors]]", "[[wiki/sources/spec-driven-limite-harness-proximo-passo]]", "[[wiki/sources/clean-architecture-custando-caro-era-ia]]"]
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

[[wiki/sources/spec-driven-limite-harness-proximo-passo]]: "O que força não é a instrução, o que força são os sensores. O agente não deve ser quem julga — quem julga tem que ser uma ferramenta que retorna 0 ou 1. Se tu deixar o agente julgar, ele vai olhar pro código e vai achar que tá bom o suficiente sem rodar o teste."

## Distribuição temporal (Böckeler)

| Momento | Sensores | Propósito |
|---------|----------|-----------|
| **Durante coding session** | Type checker, ESLint, Semgrep, dependency-cruiser, testes, GitLeaks | Feedback imediato para self-correction |
| **Pipeline CI** | Todos os acima, repetidos em ambiente limpo | Gate determinístico |
| **Drift detection (periódico)** | Security review, dependency freshness, modularity review | Detectar degradação composta |

## Sensor sidecar

Conceito emergente: ferramenta que roda sensores **em paralelo** ao agente, com duas views:
- **View humana:** dashboard visual (verde/vermelho) para situational awareness
- **View agente:** apenas falhas + mensagens customizadas de correção ("positive prompt injection")

O agente pode auto-corrigir antes que o humano sequer olhe o código. Isso reduz a carga de review.

## Agente como mantenedor dos sensores

Insight de [[wiki/sources/harness-beyond-skills-sensors]]: o agente pode **ajustar thresholds** de forma controlada. Exemplo: aumentar `max-lines` de 500 → 550 para um arquivo específico, com justificativa documentada no código. Não suprime globalmente — se o arquivo crescer de novo, o sensor re-dispara.

## Balanceamento guides vs sensors

Questão em aberto: se sensores cobrem 40% dos casos que um guide tentava prevenir, o guide pode ser deletado? Sensores são verificáveis; guides são "begging" probabilístico. Mas excesso de sensores pode levar o agente a over-engineer soluções para satisfazê-los.

## Ver também

- [[wiki/concepts/tres-camadas-coding-ia]]
- [[wiki/concepts/harness-engineering]]
- [[wiki/concepts/mutation-testing]]
- [[wiki/concepts/custo-abstracoes-era-ia]] — sensores como alternativa barata a Clean Architecture ritualística
- [[wiki/sources/harness-beyond-skills-sensors]]
- [[wiki/sources/maintainability-sensors]]
- [[wiki/sources/clean-architecture-custando-caro-era-ia]]
