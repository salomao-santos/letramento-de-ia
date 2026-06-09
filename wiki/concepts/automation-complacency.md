---
title: "Automation Complacency"
type: concept
tags: [automação, psicologia, aviação, degradação-de-skills]
created: 2026-06-08
updated: 2026-06-09
sources: ["[[wiki/sources/devs-sao-os-novos-pilotos]]", "[[wiki/sources/code-review-na-era-dos-agentes]]", "[[wiki/sources/boardroom-mercado-tecnologia-mudou]]"]
---

# Automation Complacency (Complacência por Automação)

## Definição

Fenômeno estudado na aviação há décadas. Ocorre quando o operador confia tanto no sistema automatizado que para de questionar, verificar e pensar criticamente.

## Evidências

### Na aviação
- Voo Air France 447 (2009): autopilot desconectou, pilotos não conseguiram assumir controle manual. 228 mortes.
- Pilotos com 17.844h de voo apresentam enfraquecimento em habilidades manuais
- Degradação de performance: 61% no grupo com automação vs 31% no grupo manual

### Em software
- Estudo METR: devs 19% mais lentos com IA, mas percebiam 20% mais rápidos
- Diferença de percepção: ~40 pontos percentuais
- Viés de automação em code review: conselho automatizado errado seguido a taxa 26% maior (Goddard et al., 2012)

## Manifestações em dev

- Aceitar output do agente sem revisar
- "LGTM" automático em PRs gerados por IA
- Perda de habilidade de debug manual
- Incapacidade de assumir quando a IA falha ("automation surprise")

## Viés da eloquência (Zarathon Viana)

Uma manifestação específica: LLMs são **estatisticamente eloquentes** — constroem frases (e código) articulados que geram confiança desproporcional. Na terceira ou quarta interação sem falha visível, o humano para de criticar.

> "Você vai ganhando confiança com esse negócio. Às vezes na terceira, quarta interação nem julga mais, perde o senso crítico."

A eloquência é o vetor que acelera a complacência. Code review passa a ser "LGTM" porque o código parece certo, é bem escrito, resolve. Mas não necessariamente escala ou respeita o domínio.

## Relação com a série

Conecta diretamente com:
- [[wiki/concepts/horas-de-voo-para-devs]] — antídoto: manter prática manual
- [[wiki/concepts/code-review-como-portao]] — portão contra complacência
- [[wiki/concepts/sensores-computacionais]] — cercas determinísticas independentes de confiança humana

## Ver também

- [[wiki/sources/devs-sao-os-novos-pilotos]]
- [[wiki/sources/code-review-na-era-dos-agentes]]
- [[wiki/sources/boardroom-mercado-tecnologia-mudou]] — viés da eloquência como vetor de complacência
