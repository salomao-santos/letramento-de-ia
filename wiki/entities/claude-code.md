---
title: "Claude Code"
type: entity
tags: [ferramenta, agente-coding, anthropic, terminal]
created: 2026-06-08
updated: 2026-06-09
sources: ["[[wiki/sources/as-3-camadas-do-coding-com-ia]]", "[[wiki/sources/memoria-agentes-karpathy-agentmemory]]"]
---

# Claude Code

## O que é

Agente de coding da Anthropic. Orientado a terminal, agentic-first. Forte em long-running tasks.

## Características

- Terminal-first (não é IDE)
- Suporta sub-agents e skills
- Contexto persistente via `CLAUDE.md` no root do projeto
- Modelos de fronteira pós-treinados no harness (Claude treinado sabendo que rodaria no Claude Code)

## Uso na série

Citado em todos os artigos como exemplo principal de agente de coding. Casos:
- Raquel: agente criou dependência circular entre módulos (artigo de arquitetura)
- Thomaz: agente escreveu testes que confirmavam bug (artigo de TDD)
- Bruna: gerou feature inteira com bug de regra de negócio (artigo de code review)

## Ecossistema

- Superpowers (Jesse Vincent): plugin TDD ortodoxo, 650k+ installs
- Matt Pocock Skills: skill `tdd` trending #1 GitHub

## Compaction de Contexto (3 níveis)

Análise do código-fonte ([[wiki/sources/memoria-agentes-karpathy-agentmemory|Akita, 2026]]) revela a implementação mais sofisticada de [[wiki/concepts/compaction-de-contexto|compaction]] entre os agentes:

1. **Microcompact** (temporal): limpa resultados de tools antigos após gap de 60min (sincronizado com TTL de cache)
2. **Autocompact**: summarization com 9 seções fixas — preserva todas as mensagens do usuário verbatim (seção 6)
3. **SessionMemoryCompact** (experimental): cruza com memória persistente entre sessões

Circuit breaker: para após 3 falhas consecutivas (evita ~250K API calls/dia desperdiçados).

Design philosophy: **preservar narrativa do usuário** + otimizar custo de cache.

## Ver também

- [[wiki/entities/cursor]]
- [[wiki/entities/opencode]]
- [[wiki/concepts/harness-engineering]]
- [[wiki/concepts/compaction-de-contexto]]
- [[wiki/concepts/memoria-longo-prazo-agentes]]
