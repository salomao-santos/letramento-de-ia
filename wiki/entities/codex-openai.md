---
title: "Codex (OpenAI)"
type: entity
tags: [ferramenta, agente-coding, openai]
created: 2026-06-08
updated: 2026-06-09
sources: ["[[wiki/sources/as-3-camadas-do-coding-com-ia]]", "[[wiki/sources/memoria-agentes-karpathy-agentmemory]]"]
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

## Compaction de Contexto — Handoff Explícito

Análise do código-fonte ([[wiki/sources/memoria-agentes-karpathy-agentmemory|Akita, 2026]]):

- Limite por modelo (`auto_compact_token_limit` via `ModelProviderInfo`)
- Resumo estilo **handoff para outro LLM** — 4 bullets: progresso, decisões, próximos passos, referências
- Prefixo "another language model started to solve this problem and produced a summary"
- Hooks `pre_compact` / `post_compact` em Rust (ponto de integração com ferramentas externas)

Design philosophy: **handoff entre modelos** — o resumo é escrito assumindo que outro LLM vai continuar.

## Ver também

- [[wiki/entities/claude-code]]
- [[wiki/entities/opencode]]
- [[wiki/concepts/harness-engineering]]
- [[wiki/concepts/compaction-de-contexto]]
- [[wiki/concepts/memoria-longo-prazo-agentes]]
