---
title: "Harness Engineering"
type: concept
tags: [harness-engineering, agentes-ia, ferramentas]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[wiki/sources/as-3-camadas-do-coding-com-ia]]", "[[wiki/sources/arquitetura-na-era-dos-agentes]]", "[[wiki/sources/engenharia-era-piloto-automatico]]"]
---

# Harness Engineering

## Definição

"Harness" vem de arreio de cavalo (rédea, sela, freio, bridão). O modelo é o cavalo — potente, rápido, mas sem rumo. O harness é tudo que canaliza essa potência numa direção útil.

Fórmula canônica: **Agent = Model + Harness**

Definição aceita por [[wiki/entities/martin-fowler]], OpenAI, LangChain, Anthropic e Thoughtworks.

## Componentes do Harness

### Internos (vêm com a ferramenta)
- System prompt
- Mecanismo de retrieval
- Orquestração de tools

### Externos (você constrói por cima)
- Contexto persistente: CLAUDE.md, AGENTS.md, .cursorrules
- Tools e MCPs
- Sub-agents
- Hooks
- Skills

## Distinção importante

[[wiki/entities/zarathon-viana]] argumenta que Harness Engineering na acepção da literatura (camada 2) é importante mas insuficiente. A camada que mais pesa é a engenharia de software clássica ([[wiki/concepts/tres-camadas-coding-ia]]).

## Harness como comunicação

Zarathon expande o conceito: harness não é só tooling, é também **comunicação**. A habilidade de se expressar com clareza, sem ambiguidade e de forma token-efficient é parte do harness. Quem não declara intenção de forma direta e pragmática perde tempo em pingpong com a LLM e polui o contexto.

> "Harness não é só tooling, harness também é comunicação."

## Categorias (Fowler/Böckeler)

- **Guides (feedforward):** instruções que canalizam o comportamento do agente antes da ação
- **Sensors (feedback):** verificações que detectam problemas depois da ação ([[wiki/concepts/sensores-computacionais]])

## Ver também

- [[wiki/concepts/tres-camadas-coding-ia]]
- [[wiki/concepts/ambient-affordances]]
- [[wiki/concepts/spec-driven-development]]
- [[wiki/sources/harness-engineering-fowler]] — artigo fonte original
- [[wiki/sources/maintainability-sensors]] — aplicação prática dos sensores
