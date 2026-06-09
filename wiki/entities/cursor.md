---
title: "Cursor"
type: entity
tags: [ferramenta, agente-coding, ide, editor]
created: 2026-06-08
updated: 2026-06-09
sources: ["[[wiki/sources/as-3-camadas-do-coding-com-ia]]", "[[wiki/sources/voltei-do-vale-do-silicio-dev-2026]]"]
---

# Cursor

## O que é

IDE com IA integrada. Editor-first, forte em autocomplete e chat contextual.

## Características

- Inline, integrado ao editor
- Configuração via `.cursorrules`
- Forte em autocomplete e chat contextual
- Histórico de uso marcado pelo estudo METR
- **Canvas:** feature nova para outputs visuais (diagramas, timelines, post mortems)

## Como o Cursor usa o Cursor (práticas internas)

Informações de [[wiki/sources/voltei-do-vale-do-silicio-dev-2026|relato de Waldemar Neto]] após visita ao escritório:

- **40-50% dos usuários não são devs** (designers, founders, PMs, marketing)
- Cresceram sem manager tradicional — autonomia total para priorizar backlog
- Engenheiros passam boa parte do dia em **analytics**, não código
- MCPs trazem contexto vivo do negócio (Linear, dashboards de produto)
- Code review automatizado por **t-shirt size** (pequeno passa direto, médio chama humano)
- Specs estruturadas para agentes seguirem
- MCP central com governança
- Self healing: agente arruma PRs sozinhos
- Agentes que abrem PRs para melhorar código e resolver bugs
- Projetos longos: quebrados em partes (feature full stack), cada feature dispara ~5 cloud agents simultâneos
- Critério de quebra de tasks: "menor trabalho + maior que um agente consegue sem esbarrar em outro"
- Dados de produção consultados via MCP antes de decisões de arquitetura
- Investigação de incidentes: Canvas + prompt único cruzando Datadog, Audit Logs e histórico de PRs

## Nota sobre o estudo METR

Desenvolvedores no estudo tipicamente tinham apenas algumas dezenas de horas de uso antes/durante o experimento. Pouca proficiência = pouco resultado.

## Ver também

- [[wiki/entities/claude-code]]
- [[wiki/entities/github-copilot]]
- [[wiki/concepts/tres-camadas-coding-ia]]
- [[wiki/concepts/product-engineer]]
- [[wiki/concepts/harness-engineering]]
