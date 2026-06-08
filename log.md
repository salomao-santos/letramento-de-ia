---
title: "Log de Operações"
type: log
created: 2026-06-08
updated: 2026-06-08
---

# Log de Operações

## [2026-06-08] ingest | As 3 camadas do coding com IA (série completa - 5 artigos)
- Fonte: Série "As 3 camadas do coding com IA" por Zarathon Viana (ZaraTips/Substack)
- Artigos processados:
  1. "As 3 camadas do coding com IA: onde o engenheiro de verdade ainda faz diferença" (2026-04-21)
  2. "Arquitetura de software na era dos agentes: a cerca que o LLM não pula" (2026-05-06)
  3. "Devs são os novos pilotos de avião (e ninguém tá te preparando pra isso)" (2026-04-09)
  4. "O teste que você não escreveu virou o bug que o agente escondeu" (2026-05-14)
  5. "Se teu code review é LGTM automático, o gargalo é tu, não o agente" (2026-04-09)
- Páginas criadas: 5 sources, 10 concepts, 10 entities
- Observações: Série extremamente coesa; todos os artigos convergem para a tese de que a engenharia de software clássica (camada 3) é onde o engenheiro se destaca na era da IA. Dados fortemente embasados (METR, DORA 2025, Fowler/Böckeler).

## [2026-06-08] ingest | Harness Engineering for Coding Agent Users (Böckeler/Fowler)
- Fonte: "Harness engineering for coding agent users" por Birgitta Böckeler, publicado em martinfowler.com (2026-04-01)
- Páginas criadas: wiki/sources/harness-engineering-fowler, wiki/entities/birgitta-bockeler
- Páginas atualizadas: wiki/concepts/harness-engineering, wiki/concepts/sensores-computacionais, index.md
- Observações: Artigo fundacional que define a taxonomia completa (guides/sensors × computational/inferential). É a fonte primária citada por toda a série do Zarathon Viana.

## [2026-06-08] ingest | Maintainability Sensors for Coding Agents (Böckeler)
- Fonte: "Maintainability sensors for coding agents" por Birgitta Böckeler, publicado em martinfowler.com (2026-05-26)
- Páginas criadas: wiki/sources/maintainability-sensors
- Páginas atualizadas: wiki/entities/birgitta-bockeler, wiki/concepts/mutation-testing, wiki/entities/dependency-cruiser, index.md
- Observações: Walkthrough prático com sensores reais em projeto TypeScript/NextJS. Confirma que mutation testing é crucial quando testagem é delegada à IA. Mostra que cross-file concerns precisam de sensor inferencial.

## [2026-06-08] ingest | Understanding Spec-Driven-Development: Kiro, spec-kit, and Tessl (Böckeler)
- Fonte: "Understanding Spec-Driven-Development: Kiro, spec-kit, and Tessl" por Birgitta Böckeler, publicado em martinfowler.com (2026)
- Páginas criadas: wiki/sources/spec-driven-development, wiki/concepts/spec-driven-development, wiki/entities/kiro-ide
- Páginas atualizadas: index.md
- Observações: Análise crítica das 3 ferramentas SDD. Define 3 níveis (spec-first, spec-anchored, spec-as-source). Levanta preocupação com "Verschlimmbesserung" — piorar na tentativa de melhorar. Paralelo interessante com MDD do passado.

## [2026-06-08] synthesis | Engenharia de Software na Era dos Agentes de IA
- Tipo: Síntese/Overview
- Páginas criadas: wiki/synthesis/overview-engenharia-na-era-ia
- Páginas atualizadas: index.md
- Fontes sintetizadas: 8 (todas as fontes disponíveis na wiki)
- Observações: Conecta a série do Zarathon Viana com o trabalho da Böckeler/Fowler. Identifica a tese central (IA como amplificador), o framework de 3 camadas, os 3 pilares, o gradiente determinístico→probabilístico, dados de suporte, contradições e lacunas.
