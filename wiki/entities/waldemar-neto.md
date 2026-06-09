---
title: "Waldemar Neto"
type: entity
tags: [pessoa, autor, engenharia-de-software, brasil, tech-leads-clube]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[wiki/sources/spec-driven-limite-harness-proximo-passo]]", "[[wiki/sources/spec-driven-guia-completo-waldemar]]", "[[wiki/sources/voltei-do-vale-do-silicio-dev-2026]]", "[[wiki/sources/clean-architecture-custando-caro-era-ia]]"]
---

# Waldemar Neto

## Quem é

Engenheiro de software brasileiro, fundador do **Tech Leads Clube** (@techleadsclub). Foco em liderança técnica, desenvolvimento assistido por IA e práticas de engenharia escaláveis. Promove workshops sobre desenvolvimento com agentes (incluindo "Desenvolvimento Assistido por IA Avançado").

## Contribuição principal

Série de vídeos sobre Spec-Driven Development, Harness Engineering e Product Engineer no canal do Tech Leads Clube. Combina visão prática (tutorial) com análise crítica (limitações). Viajou ao Vale do Silício e trouxe relatos de empresas como Cursor, Stripe, Databricks e Try.

## Posições-chave

- Spec Driven é subset de Harness: cobre feed forward (guias) mas não feedback (sensores), memória entre sessões nem orquestração multi-agente
- RPI (Research → Plan → Implement): separar fases em janelas de contexto diferentes para economizar tokens e evitar poluição
- Orquestração multi-agente com contrato (Build + QA em processos separados) — evita loop infinito
- Framework PBQ: harness sobre spec-driven com sprints, progress files e evaluation loop
- Agente não deve ser self-judge — precisa de processo externo de validação
- Janela de contexto ≤ 200K tokens como regra prática (mesmo com 1M disponível)
- Subagents para paralelização — 4 simultâneos em caso real, janela principal em 50K tokens
- Analogia GPS: feed forward = rota, feedback = recálculo de rota
- 6 falhas de agentes (Anthropic): spec cobre 2 de 6 completamente
- Custo real: 51 centavos para todo-list completa com QA loop
- Clean Architecture ritualística tem custo mensurável em tokens/acurácia — princípios válidos, cerimônia não
- "Estratégico primeiro, flat depois, abstrai por dor" — regra para times
- DDD Estratégico (bounded context, linguagem ubíqua) ficou mais importante com IA; DDD tático vale questionar peça por peça
- Encapsulamento ≠ Inversão de dependência — confusão gera over-engineering
- YAGNI escalado: IA gera abstração preventiva em minutos, custo aparece depois
- Paper Navigation Paradox (2026): agente perde 1 em 4 arquivos com DI escondida

## Ferramentas/Skills

- **TLC Spec Driven** (skill do Tech Leads Clube, criada por Felipe Rodrigues): skill flexível de spec-driven development
- **PBQ Framework**: implementação experimental de harness completo sobre spec-driven

## Posições-chave (vídeo Vale do Silício)

- **Product Engineer** = "constrói a coisa que constrói a coisa" — perfil em alta demanda
- Duas faces inseparáveis: senso de produto (taste, PM, analytics) + harness/qualidade
- IA acelera quem já tem **alavanca** — construir alavanca é a habilidade #1
- Dev profissional no Vale virou orquestrador com autonomia total (sem manager tradicional)
- Gap Brasil × Vale é oportunidade: quem se posiciona ganha 1-2 anos de vantagem
- Taste: julgamento estético e de qualidade sem regra ou demanda explícita
- 4 movimentos práticos: mentalidade de produto, reunião com PM, peça de harness, system design

## Publicações nesta wiki

- [[wiki/sources/spec-driven-limite-harness-proximo-passo]]
- [[wiki/sources/spec-driven-guia-completo-waldemar]]
- [[wiki/sources/voltei-do-vale-do-silicio-dev-2026]]
- [[wiki/sources/clean-architecture-custando-caro-era-ia]]

## Links

- Substack: @techleadsclub
- Circle: Tech Leads Club (discover.circle.so)
