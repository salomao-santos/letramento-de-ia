---
title: "Codex (OpenAI)"
type: entity
tags: [ferramenta, agente-coding, openai]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[wiki/sources/as-3-camadas-do-coding-com-ia]]"]
---

# Codex (OpenAI)

## O que é

Agente de coding da OpenAI. Agent-first, roda em ambiente isolado. Bom para task-oriented work.

## Características

- Roda em ambiente isolado (sandbox)
- GPT-5 pós-treinado no harness do Codex
- Forte em execução de tarefas bem definidas
- OpenAI construiu aplicação de produção com 1M+ linhas sem código escrito por humanos

## Nota sobre acoplamento

O Codex é tão acoplado ao seu harness que o OpenCode precisou adicionar uma ferramenta `apply_patch` especificamente para modelos GPT/Codex, imitando o harness do Codex.

## Ver também

- [[wiki/entities/claude-code]]
- [[wiki/entities/opencode]]
- [[wiki/concepts/harness-engineering]]
