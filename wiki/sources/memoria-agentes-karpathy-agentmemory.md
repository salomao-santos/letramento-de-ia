---
title: "Memória de Agentes IA: Karpathy LLM Wiki e agentmemory na Prática"
type: source
tags: [memoria, contexto, compaction, llm-wiki, agentmemory, mcp]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[raw/clippings/Memória de Agentes IA Karpathy LLM Wiki e agentmemory na Prática]]"]
---

# Memória de Agentes IA: Karpathy LLM Wiki e agentmemory na Prática

## Metadados

- **Autor:** [[wiki/entities/fabio-akita|Fabio Akita]]
- **Publicado:** 2026-05-18
- **Fonte:** https://akitaonrails.com/2026/05/18/memoria-agentes-karpathy-llm-wiki-agentmemory/
- **Atualização:** 2026-05-23 — autor abandonou agentmemory por bugs (BM25 reindex, janela de perda de dados, hook errado em ~47% das tool calls) e criou substituto em Rust chamado **ai-memory**

## Resumo

Mergulho técnico no funcionamento interno de memória dos três principais agentes de coding (Claude Code, Codex CLI, opencode), com análise do código-fonte de cada um. Explica o problema de janela de contexto, como compaction funciona em cada agente, e apresenta o padrão **LLM Wiki** do Karpathy como solução para memória de longo prazo. Fecha com walkthrough prático do agentmemory como implementação MCP do padrão.

## Pontos-chave

### Contexto e Compaction

- LLMs não têm memória persistente — tudo é texto na janela de contexto
- Quando a janela enche, todos os agentes implementam **compaction**: resumem a conversa via chamada LLM extra e descartam o histórico bruto
- Trade-off fundamental: compaction libera espaço mas destrói memória de longo prazo

### Comparação de Compaction nos 3 Agentes

| Aspecto | Claude Code | Codex CLI | opencode |
|---------|------------|-----------|----------|
| Tipos de compaction | 3 (microcompact, autocompact, sessionMemoryCompact) | 1 (+ variantes remote) | 1 (anchored, atualizável) |
| Buffer pré-compaction | 13K + 20K tokens | por modelo | 20K tokens |
| Estrutura do summary | 9 seções fixas (preserva todas msgs do usuário verbatim) | 4 bullets (handoff-style) | Atualização incremental do anchored summary |
| Circuit breaker | Sim (3 falhas param ciclo) | Não | Não |
| Hooks | PreCompact / PostCompact | pre_compact / post_compact | Sem hooks |
| Microcompact temporal | Sim (60min, sincronizado com TTL cache) | Não | Não |

### Design Philosophies

- **Claude Code**: preserva narrativa do usuário (seção 6: lista verbatim todas as mensagens) + otimiza custo de cache
- **Codex CLI**: handoff entre modelos (resumo é tratado como "produzido por outro LLM")
- **opencode**: summarização incremental (anchored summary atualizado, não regenerado)

### Padrão LLM Wiki (Karpathy)

Proposto por [[wiki/entities/andrej-karpathy|Andrej Karpathy]] em abril de 2026. Arquitetura em 3 camadas:

1. **Raw Sources** — documentos imutáveis (source of truth)
2. **Wiki Layer** — páginas markdown geradas/mantidas pelo LLM, interligadas
3. **Schema** — convenções e taxonomia (como CLAUDE.md)

Operações: **Ingest** (extrair e cross-referenciar), **Query** (sintetizar com citações), **Lint** (detectar contradições e lacunas)

Vantagem sobre RAG: **conhecimento compõe** — wiki sintetiza uma vez, queries partem da síntese, não dos brutos.

### agentmemory — Implementação Prática

- Daemon Node local (SQLite + index vetorial) com servidor MCP (51 tools)
- Retrieval híbrida: BM25 + vetor + knowledge graph (fusão RRF, k=60)
- **4-tier memory consolidation** (inspirada no cérebro): Working → Episodic → Semantic → Procedural
- Decay (Ebbinghaus curve), reforço, eviction, detecção de contradições
- 12 hooks pra Claude Code, 6 pra Codex
- Serve múltiplos agentes do mesmo daemon (handoff sem fricção)

> [!warning] Deprecação parcial
> O autor abandonou agentmemory após 1 semana em produção (bugs críticos) e criou **ai-memory** em Rust. O padrão conceitual continua válido; a implementação específica tem problemas.

### Vendor Lock é Mito

- Memória de agente é **texto** — não há formato proprietário
- Handoff manual entre agentes funciona (exportar contexto para markdown)
- Com camada MCP compartilhada, os agentes lêem do mesmo lugar

## Modelo de 4 Camadas para Memória

1. **Compaction** — resolve janela cheia (automática, todos os agentes fazem)
2. **Markdown manual em `.docs/`** — fallback básico, exige disciplina
3. **LLM Wiki** (Karpathy) — workflow estruturado com ingest/query/lint
4. **agentmemory / MCP** — automatiza a wiki, adiciona consolidation e retrieval híbrida

## Dados Técnicos Relevantes

- Opus 4.7: janela de 1M tokens; GPT 5.5: janela de 1M tokens
- Claude Code circuit breaker: 1.279 sessões tinham 50+ falhas consecutivas (até 3.272), desperdiçando ~250K API calls/dia globalmente
- agentmemory: R@5 95.2% retrieval, 92% fewer tokens, 53 MCP tools, 950+ tests

## Referências

- [[wiki/concepts/compaction-de-contexto]]
- [[wiki/concepts/llm-wiki-karpathy]]
- [[wiki/concepts/memoria-longo-prazo-agentes]]
- [[wiki/entities/fabio-akita]]
- [[wiki/entities/andrej-karpathy]]
- [[wiki/entities/agentmemory]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/opencode]]
- [[wiki/entities/codex-openai]]
