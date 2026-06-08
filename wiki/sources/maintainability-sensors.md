---
title: "Maintainability sensors for coding agents"
type: source
tags: [sensores-computacionais, linting, mutation-testing, dependency-cruiser, modularity]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[raw/clippings/Maintainability sensors for coding agents]]"]
author: "Birgitta Böckeler"
published: 2026-05-26
---

# Maintainability Sensors for Coding Agents

## Resumo

Artigo prático da Birgitta Böckeler (Thoughtworks) que demonstra experimentação detalhada com sensores de manutenibilidade em um projeto real (dashboard de analytics em TypeScript/NextJS/React). Detalha ESLint, dependency-cruiser, métricas de acoplamento, AI modularity review e mutation testing como ferramentas para controlar qualidade de código gerado por agentes.

## Tese Central

Problemas de qualidade interna afetam agentes de IA de forma similar a humanos. Sensores computacionais no nível de arquivo/função impressionam; cross-file concerns precisam de sensores inferenciais (IA) para interpretação semântica.

## Distribuição dos Sensores

### Durante a sessão de coding
- Type checker (computacional)
- ESLint (computacional)
- Semgrep - SAST (computacional)
- dependency-cruiser - regras estruturais (computacional)
- Test suite + coverage (computacional)
- Mutation testing incremental (computacional)
- GitLeaks no pre-commit hook (computacional)

### Pós-integração (pipeline)
- Todos os computacionais acima repetidos em CI limpo

### Periodicamente (drift)
- Security review (inferencial)
- Data handling review (inferencial)
- Dependency freshness report (computacional + inferencial)
- Modularity and coupling review (computacional + inferencial)

## Aprendizados com ESLint

### Regras para falhas típicas de IA
- Max arguments para funções
- File length / function length
- Cyclomatic complexity
- Não estavam ativas no preset padrão!

### Guidance para auto-correção
Custom formatter com mensagens expandidas = "prompt injection positiva". Exemplo: para `no-explicit-any`, a mensagem diz ao agente para fazer julgamento e suprimir se justificado.

### Observações-chave
- Exceções criadas pela IA = bom ponto de partida para code review humano
- Sem guidance explícita, IA prefere aumentar threshold de complexidade
- Custom lint messages fazem diferença real no comportamento do agente

## Dependency Rules (dependency-cruiser)

Regras de dependência entre camadas (routes → services → clients + domain). Mensagens de erro expandidas com contexto da estrutura de camadas.

### Aprendizado principal
> "Replacement útil para descrever estrutura de código em markdown guide. Porém limitado ao que é expressável via imports, nomes de arquivo e pastas."

## Coupling Analysis

### Métricas computacionais puras → limitadas
- Padrões legítimos aparecem como "god classes" (ex: factory de DI, schema compartilhado)
- Dados de acoplamento brutos são ruidosos sem interpretação semântica

### AI Modularity Review → muito mais útil
Usando "Modularity Skills" (Vlad Khononov). Achados reais:
- Código de rota duplicado entre endpoints
- Inconsistência em chamadas ao backend
- 40+ arquivos afetados por mudança que deveria ser simples
- Responsabilidades no lugar errado

> "Sem review humano E sem reviews extras de IA, o agente estava definitivamente acumulando dívida técnica inadvertida."

## Mutation Testing como Sensor de Regressão

### O problema
Coverage alta ≠ testes efetivos. 100% statement coverage com 75% branch coverage → 13 mutantes sobreviventes. Coverage diz que a linha executou, não que o impacto foi verificado.

### Stryker (ferramenta usada)
- Resultados em JSON grande → script customizado para queries
- IA muito boa em analisar hotspots e priorizar melhorias
- Não roda continuamente (muito pesado) → runs incrementais manuais

### Tendência atual
Testes end-to-end/acceptance ficando populares (IA gera bem). Mutation testing ajuda monitorar o gap entre coverage e efetividade real.

## Conclusões do artigo

1. Sensores computacionais impressionam no nível arquivo/função
2. Cross-file (modularity, coupling) precisa de sensor inferencial
3. Conflitos entre sensores são uma questão emergente
4. Mutation testing é crucial quando testagem é delegada à IA
5. Não é solução mágica para tirar humano do loop
6. Melhora significativa na experiência de review e nível de confiança

## Conceitos Relacionados

- [[wiki/concepts/sensores-computacionais]]
- [[wiki/concepts/mutation-testing]]
- [[wiki/concepts/harness-engineering]]
- [[wiki/entities/dependency-cruiser]]
- [[wiki/entities/birgitta-bockeler]]
- [[wiki/sources/harness-engineering-fowler]]

## Referências

- Artigo original: https://martinfowler.com/articles/sensors-for-coding-agents.html
- dependency-cruiser: https://github.com/sverweij/dependency-cruiser
- Stryker Mutator: https://stryker-mutator.io/
- Vlad Khononov Modularity Skills: https://github.com/vladikk/modularity
- Factory ESLint Plugin: https://github.com/Factory-AI/eslint-plugin
