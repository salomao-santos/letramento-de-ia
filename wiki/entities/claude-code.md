---
title: "Claude Code"
type: entity
tags: [ferramenta, agente-coding, anthropic, terminal]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[wiki/sources/as-3-camadas-do-coding-com-ia]]"]
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

## Ver também

- [[wiki/entities/cursor]]
- [[wiki/entities/opencode]]
- [[wiki/concepts/harness-engineering]]
