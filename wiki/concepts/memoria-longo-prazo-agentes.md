---
title: "Memória de Longo Prazo para Agentes"
type: concept
tags: [memoria, agentes, persistencia, mcp, consolidacao]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[wiki/sources/memoria-agentes-karpathy-agentmemory]]", "[[wiki/sources/spec-driven-limite-harness-proximo-passo]]"]
---

# Memória de Longo Prazo para Agentes

## Definição

Mecanismos que permitem a agentes de coding reter conhecimento além de uma única sessão ou ciclo de [[wiki/concepts/compaction-de-contexto|compaction]]. Sem memória de longo prazo, decisões tomadas no início de sessões longas evaporam quando compaction descarta o histórico bruto.

## O problema

Compaction resolve o problema imediato (espaço no contexto) mas cria um problema sutil: **informação do início da sessão é eliminada primeiro**. Se você explorou uma arquitetura por 30 minutos, decidiu trade-offs e descartou abordagens, no turno 50 essa exploração pode ter virado uma linha de bullet point. Perguntas como "por que decidimos não usar Redis aqui?" ficam sem resposta.

[[wiki/sources/spec-driven-limite-harness-proximo-passo]] categoriza isso como falha #3 de agentes: "amnésia entre sessões". Cada nova sessão começa do zero — como equipe de turnos sem passagem de bastão. O agente gasta metade dos tokens tentando entender o que aconteceu. A spec diz o que fazer, mas não o que foi feito, o que deu errado e qual o estado atual. Solução: progress files + disciplina de git + scripts de bootstrap que reconstruam contexto.

## Modelo de 4 Camadas (progressivo)

| Camada | O que resolve | Custo |
|--------|--------------|-------|
| 1. Compaction automática | Janela de contexto cheia | Perda de detalhe (automático) |
| 2. Markdown manual (`.docs/`) | Decisões importantes não evaporam | Disciplina humana |
| 3. LLM Wiki (Karpathy) | Estrutura + cross-referência + lint | Setup + schema |
| 4. MCP externo (agentmemory) | Automatização completa + multi-agente | Daemon permanente + API de embedding |

Cada camada é progressivamente mais sofisticada e resolve limitações da anterior.

## Vendor Lock é mito

Memória de agente é **texto**. Não há formato proprietário binário nem state secreto. Formas de handoff entre agentes:

- **Manual:** exportar contexto para markdown (HANDOFF.md), abrir outro agente, mandar ler
- **Via MCP compartilhado:** múltiplos agentes lêem do mesmo daemon de memória
- **Exportar contexto é melhor que confiar na compaction**: você decide quando e o que preservar

## Consolidação em 4 Tiers (inspiração neurocientífica)

Implementada pelo [[wiki/entities/agentmemory|agentmemory]], inspirada em processamento de memória durante o sono:

1. **Working** — observações brutas capturadas em tempo real
2. **Episodic** — resumos de sessão (o que aconteceu)
3. **Semantic** — fatos e padrões extraídos (o que isso significa)
4. **Procedural** — workflows e padrões de decisão (como fazer)

Inclui: decay (curva de Ebbinghaus), reforço por acesso, eviction de stale, resolução de contradições.

## Efeito composto

A parte mais subestimada: uma decisão arquitetural salva hoje fica disponível para todas as sessões futuras, em qualquer agente. Uma pegadinha de biblioteca descoberta na terça não precisa ser redescoberta no domingo. Demora algumas semanas para engatar (precisa de massa crítica de memórias salvas), mas muda o jogo.

## Práticas recomendadas

1. **Mínimo:** manter `CLAUDE.md` ou `.docs/` no root com decisões importantes
2. **Intermediário:** forçar agente a consultar memória no início de tasks não-triviais
3. **Avançado:** daemon MCP + hooks automáticos em compaction + consolidação periódica

## Ver também

- [[wiki/concepts/compaction-de-contexto]]
- [[wiki/concepts/llm-wiki-karpathy]]
- [[wiki/entities/agentmemory]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/codex-openai]]
- [[wiki/entities/opencode]]
