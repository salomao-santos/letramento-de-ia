---
title: "Compaction de Contexto"
type: concept
tags: [memoria, contexto, agentes, llm, compaction]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[wiki/sources/memoria-agentes-karpathy-agentmemory]]"]
---

# Compaction de Contexto

## Definição

Mecanismo pelo qual agentes de coding resumem o histórico de conversa quando a janela de contexto se aproxima do limite. Uma chamada LLM extra produz um resumo compacto, o histórico bruto é descartado, e a sessão continua a partir do resumo.

## Por que existe

LLMs não têm memória persistente. Tudo que o modelo "lembra" são tokens na janela de contexto. Cada mensagem, arquivo lido, saída de comando e tool call consome espaço. Quando a janela enche:

- Performance degrada (informação relevante fica enterrada)
- Custo sobe (mais tokens = mais caro)
- Latência aumenta (janelas grandes = inferência mais lenta)

## Como funciona (padrão geral)

1. Agente monitora uso de tokens a cada turno
2. Quando atinge threshold (ex: limite - buffer de 13-20K tokens), dispara compaction
3. Prompt especial de summarization é enviado ao LLM com o histórico
4. LLM produz resumo estruturado
5. Histórico bruto é descartado
6. Sessão continua com resumo como "memória"

## Trade-off fundamental

**Ganho:** mais espaço para trabalhar, custo menor, latência menor
**Custo:** perda de detalhe — decisões, trade-offs descartados e explorações ficam reduzidos a bullets

> [!warning] Problema central
> Informação do início da sessão é eliminada primeiro. Decisões tomadas há 30 minutos podem virar uma linha genérica. É por isso que [[wiki/concepts/memoria-longo-prazo-agentes|memória de longo prazo]] precisa de solução externa.

## Implementações por agente

### Claude Code — 3 níveis

1. **Microcompact** (temporal): limpa resultados de tools antigos após gap de 60min (sincronizado com TTL de cache do servidor)
2. **Autocompact**: summarization com 9 seções fixas; preserva todas as mensagens do usuário verbatim
3. **SessionMemoryCompact** (experimental): cruza com memória persistente entre sessões

Circuit breaker: para após 3 falhas consecutivas. Sem isso, 1.279 sessões tinham 50+ falhas consecutivas (~250K API calls/dia desperdiçados globalmente).

### Codex CLI — handoff explícito

- Limite por modelo (`auto_compact_token_limit`)
- Resumo estilo "handoff para outro LLM" — 4 bullets: progresso, decisões, próximos passos, referências
- Hooks `pre_compact` / `post_compact` em Rust

### opencode — summarização ancorada

- Buffer de 20K tokens
- "Anchored summary" **atualizado** a cada compaction (não regenerado do zero)
- Turnos recentes ficam verbatim fora do resumo
- Config: `compaction.auto` pode ser desabilitado

## Relação com outros conceitos

- É o mecanismo que cria a necessidade de [[wiki/concepts/memoria-longo-prazo-agentes]]
- [[wiki/concepts/llm-wiki-karpathy]] é uma solução para o que se perde na compaction
- [[wiki/concepts/harness-engineering]] pode usar hooks de compaction como ponto de integração

## Ver também

- [[wiki/entities/claude-code]]
- [[wiki/entities/codex-openai]]
- [[wiki/entities/opencode]]
- [[wiki/entities/agentmemory]]
