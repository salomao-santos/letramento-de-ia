---
title: "agentmemory"
type: entity
tags: [ferramenta, mcp, memoria, open-source, node]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[wiki/sources/memoria-agentes-karpathy-agentmemory]]"]
---

# agentmemory

## O que é

Servidor MCP open-source (Apache-2.0) que implementa memória persistente para agentes de coding. Criado por Rohit Ghumare. Implementação prática do padrão [[wiki/concepts/llm-wiki-karpathy|LLM Wiki]] com extensões (confidence scoring, lifecycle de memórias, knowledge graph, hybrid search).

## Arquitetura

- **Daemon Node** local em `127.0.0.1:3111` (REST) e `:3113` (viewer web)
- **Storage:** SQLite + index vetorial em memória (zero dependência externa)
- **Servidor MCP** (`@agentmemory/mcp`) via stdio — 51+ tools de memória
- **Plugins de hooks:** 12 para Claude Code, 6 para Codex
- **Retrieval híbrida:** BM25 + vetor + knowledge graph, fusão RRF (k=60), diversificação por sessão

## 4-Tier Memory Consolidation

Inspirada em processamento cerebral durante o sono:

1. **Working** — observações brutas em tempo real
2. **Episodic** — resumos de sessão
3. **Semantic** — fatos e padrões extraídos
4. **Procedural** — workflows e padrões de decisão

Inclui decay (curva Ebbinghaus), reforço por acesso, eviction, detecção de contradições.

## Números

- R@5: 95.2% retrieval accuracy
- 92% fewer tokens (vs context completo)
- 53 MCP tools
- 12 auto hooks
- 0 external DBs
- 950+ tests passing

## Compatibilidade

Funciona com qualquer agente MCP-compatível: Claude Code, Codex CLI, opencode, Cursor, Gemini CLI.

> [!warning] Status (maio 2026)
> [[wiki/entities/fabio-akita|Fabio Akita]] reportou bugs críticos após 1 semana em produção: BM25 reindex a cada restart, janela de 5s de perda de dados, hook errado em ~47% das tool calls do Claude Code. Criou substituto **ai-memory** em Rust. O conceito é sólido; a implementação específica tem problemas de maturidade.

## Instalação

```bash
npm install -g @agentmemory/agentmemory
agentmemory                    # sobe daemon em :3111
agentmemory connect claude-code  # configura agente
```

## Ver também

- [[wiki/concepts/llm-wiki-karpathy]]
- [[wiki/concepts/memoria-longo-prazo-agentes]]
- [[wiki/concepts/compaction-de-contexto]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/codex-openai]]
- [[wiki/entities/opencode]]
