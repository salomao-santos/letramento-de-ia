---
title: "OpenCode"
type: entity
tags: [ferramenta, agente-coding, open-source, agnóstico]
created: 2026-06-08
updated: 2026-06-09
sources: ["[[wiki/sources/as-3-camadas-do-coding-com-ia]]", "[[wiki/sources/memoria-agentes-karpathy-agentmemory]]"]
---

# OpenCode

## O que é

Agente de coding open-source que roda no terminal. Agnóstico de provider: suporta Anthropic, OpenAI, Google, Bedrock, Groq, Azure, OpenRouter, ou modelo local.

## Números (2026)

- 140 mil+ estrelas no GitHub
- 6,5 milhões de devs mensais

## Filosofia

Ser agnóstico de provider. Num mundo onde preços de modelos vão subir, não se prender é hedge estratégico.

## Trade-offs

- ✅ Flexibilidade total de provider
- ✅ Custo potencialmente menor
- ❌ Exige mais configuração
- ❌ Menos "mágica pronta" que Claude Code

## Site

- https://opencode.ai/

## Compaction de Contexto — Summarização Ancorada

Análise do código-fonte ([[wiki/sources/memoria-agentes-karpathy-agentmemory|Akita, 2026]]):

- Buffer de 20K tokens (config `compaction.reserved`)
- "Anchored summary" **atualizado** a cada compaction (não regenerado do zero)
- Turnos recentes ficam verbatim fora do resumo
- Sem hooks de compaction explícitos
- `compaction.auto` pode ser desabilitado via config

Design philosophy: **summarização incremental** — o resumo evolui a cada ciclo.

## Ver também

- [[wiki/entities/claude-code]]
- [[wiki/concepts/tres-camadas-coding-ia]]
- [[wiki/concepts/compaction-de-contexto]]
- [[wiki/concepts/memoria-longo-prazo-agentes]]
