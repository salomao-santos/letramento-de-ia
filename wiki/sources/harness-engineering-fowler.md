---
title: "Harness engineering for coding agent users"
type: source
tags: [harness-engineering, sensores-computacionais, guides, feedback, feedforward]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[raw/clippings/Harness engineering for coding agent users]]"]
author: "Birgitta Böckeler"
published: 2026-04-01
---

# Harness Engineering for Coding Agent Users

## Resumo

Artigo fundacional publicado no site do Martin Fowler que define o modelo mental de harness engineering para usuários de agentes de coding. Apresenta a taxonomia completa de guides (feedforward) e sensors (feedback), distinguindo entre elementos computacionais e inferenciais.

## Tese Central

Um harness bem construído serve dois objetivos: aumenta a probabilidade do agente acertar de primeira, e fornece um loop de feedback que auto-corrige problemas antes de chegarem aos olhos humanos.

## Modelo Mental

### Agent = Model + Harness

O harness tem dois bounded contexts:
1. **Builder harness** — construído pelo criador da ferramenta (system prompt, retrieval, orquestração)
2. **User harness** — construído pelo usuário para seu caso de uso específico

### Computational vs Inferential

| Tipo | Execução | Velocidade | Confiabilidade |
|------|----------|-----------|----------------|
| Computational | CPU, determinístico | Milissegundos a segundos | Alta |
| Inferential | GPU/NPU, semântico | Mais lento, mais caro | Não-determinístico |

### Guides (feedforward) — Antes da ação

Aumentam a probabilidade de bons resultados:
- AGENTS.md, Skills (inferencial)
- Scripts de bootstrap, codemods (computacional)
- Language Servers, CLIs (computacional)

### Sensors (feedback) — Depois da ação

Detectam problemas e alimentam auto-correção:
- Testes, linters, type checkers, análise estática (computacional)
- Review agents, "LLM as judge" (inferencial)

## Categorias de Regulação

### 1. Maintainability Harness
Regulamenta qualidade interna do código. A categoria mais fácil de implementar atualmente por ter muito tooling pré-existente.

### 2. Architecture Fitness Harness
Define e verifica características arquiteturais. Basicamente: Fitness Functions.

### 3. Behaviour Harness
O "elefante na sala" — como guiar e verificar se a aplicação se comporta como esperado funcionalmente. Ainda muito a ser resolvido nesta área.

## Harnessability

Nem toda codebase é igualmente harnessável:
- Linguagens com tipagem forte → type checking como sensor natural
- Fronteiras de módulo definíveis → regras de arquitetura possíveis
- Greenfield → pode embutir harnessability desde dia 1
- Legacy com dívida técnica → harness mais necessário onde é mais difícil de construir

## Harness Templates

Bundles de guides e sensors atrelados a topologias de serviço padronizadas. Times podem escolher tech stacks parcialmente baseados em quais harnesses já existem para eles.

## Timing: Keep Quality Left

Distribuir sensors ao longo do lifecycle:
- **Antes de commit:** linters, testes rápidos, code review agent básico
- **Pós-integração no pipeline:** mutation testing, review mais amplo
- **Contínuo (drift):** dead code, qualidade de cobertura, dependency scanners
- **Runtime:** SLOs degradando, anomalias em logs

## Steering Loop

O trabalho do humano é **iterar no harness**: sempre que um problema ocorre múltiplas vezes, os controles devem ser melhorados para torná-lo menos provável no futuro.

## Exemplos do mercado

- **OpenAI:** arquitetura em camadas com linters customizados e testes estruturais + "garbage collection" periódica
- **Stripe (Minions):** pre-push hooks com heurísticas, "shift feedback left", blueprints
- **Thoughtworks:** tackling architecture drift com mix de agentes e linters customizados

## Questões em aberto

- Como manter harness coerente quando cresce (guides e sensors em sync)?
- Como confiar que agentes fazem trade-offs sensatos quando instruções conflitam?
- Se sensors nunca disparam: alta qualidade ou detecção inadequada?
- Necessidade de "harness coverage" análogo a code coverage

## Conceitos Relacionados

- [[wiki/concepts/harness-engineering]]
- [[wiki/concepts/sensores-computacionais]]
- [[wiki/concepts/ambient-affordances]]
- [[wiki/concepts/tres-camadas-coding-ia]]
- [[wiki/entities/birgitta-bockeler]]

## Referências

- Artigo original: https://martinfowler.com/articles/harness-engineering.html
- LangChain Agent Harness: https://blog.langchain.com/the-anatomy-of-an-agent-harness/
- Anthropic Effective Harnesses: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- OpenAI Harness Engineering: https://openai.com/index/harness-engineering/
- Stripe Minions: https://stripe.dev/blog/minions-stripes-one-shot-end-to-end-coding-agents
