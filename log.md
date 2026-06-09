---
title: "Log de Operações"
type: log
created: 2026-06-08
updated: 2026-06-09
---

# Log de Operações

## [2026-06-09] ingest | Full Walkthrough: Workflow for AI Coding (Matt Pocock)
- Fonte: "Full Walkthrough: Workflow for AI Coding" por Matt Pocock, workshop (2025-06-09), YouTube (~1h36min)
- Páginas criadas: wiki/sources/full-walkthrough-workflow-ai-coding
- Páginas atualizadas: wiki/entities/matt-pocock (workflow completo, Sandcastle, novas skills), wiki/concepts/compaction-de-contexto (Clear > Compact), wiki/concepts/tdd-como-especificacao (TDD no Ralph loop, demonstração prática), wiki/concepts/spec-driven-development (reforço da crítica prática), wiki/concepts/ambient-affordances (demonstração skill Improve Architecture), index.md
- Observações: Workshop hands-on que operacionaliza a palestra teórica anterior. Contribuições novas: smart zone/dumb zone (~100K threshold), Clear > Compact (modelo Memento), Kanban com blocking como DAG paralelizável, AFK vs human-in-the-loop como taxonomia de tarefas, Ralph loop (script bash para implementação cíclica), Sandcastle (paralelização Docker com implementer/reviewer/merger), Push vs Pull para coding standards, doc rot como anti-padrão, QA como imposição de taste. Reforça fortemente: vertical slices, TDD essencial para AFK, deep modules, design concept via grill.

## [2026-06-09] ingest | Boardroom 2606-01: O Mercado de Tecnologia Mudou (Santos & Viana)
- Fonte: "Boardroom 2606-01: O Mercado de Tecnologia Mudou" por Salomão Santos e Zarathon Viana, canal Prodops (2026-06-26), YouTube
- Páginas criadas: wiki/sources/boardroom-mercado-tecnologia-mudou
- Páginas atualizadas: wiki/entities/zarathon-viana (posições-chave expandidas, nova fonte), wiki/concepts/automation-complacency (viés da eloquência), wiki/concepts/formacao-novos-engenheiros (nova fonte), wiki/concepts/code-review-como-portao (nova fonte), wiki/concepts/multimodelo-slm (ecos, EVAL com modelo diferente), index.md
- Observações: Podcast com visão Brasil-first (consultoria × mercado). Contribuições novas: "viés da eloquência" como vetor de automation complacency, "Build to Learn vs Build to Earn" como framework dual, onboarding 10x com IA (ler código legado), 3 pilares (DDD + Software Design + System Thinking), EM+PM convergindo, "código ≠ engenharia" como distinção do momento. Reforça fortemente teses existentes (checkpoints, TDD, code review, spec-driven não pronto).

## [2026-06-09] ingest | Harness Engineering Beyond Skills: Using Sensors (Böckeler & Ford)
- Fonte: "Harness engineering beyond skills: Using sensors to keep your coding agent in check" por Birgitta Böckeler e Chris Ford, vídeo (2026-06-08), YouTube
- Páginas criadas: wiki/sources/harness-beyond-skills-sensors
- Páginas atualizadas: wiki/concepts/harness-engineering (inner/outer harness, investimento contínuo), wiki/concepts/sensores-computacionais (distribuição temporal, sensor sidecar, agente modificando sensores, balanceamento), wiki/concepts/mutation-testing (limitação de custo, caso real coverage vs mutantes), wiki/entities/birgitta-bockeler, wiki/sources/maintainability-sensors (cross-ref), index.md
- Observações: Versão em vídeo/conversa do artigo "Maintainability sensors". Contribuições novas: clarificação terminológica inner/outer harness, experimento comparativo com/sem sensores (Haiku), conceito de sensor sidecar, agente auto-ajustando thresholds, "TDD theater", ideia de harness templates por topologia. Chris Ford traz perspectiva complementar sobre "renaissance" da static analysis e risco de superstição com guides.

## [2026-06-09] ingest | Software Fundamentals Matter More Than Ever (Matt Pocock)
- Fonte: "Software Fundamentals Matter More Than Ever" por Matt Pocock, palestra em conferência (2025-06-08), YouTube
- Páginas criadas: wiki/sources/software-fundamentals-matter-more-than-ever, wiki/entities/matt-pocock
- Páginas atualizadas: wiki/concepts/llm-wiki-karpathy (ubiquitous language como micro-wiki), wiki/concepts/spec-driven-development (crítica prática a specs-to-code), wiki/concepts/tdd-como-especificacao (TDD como limite de velocidade), wiki/concepts/ambient-affordances (deep modules), wiki/concepts/harness-engineering (design concept e ubiquitous language como guides), index.md
- Observações: Palestra que converge com teses existentes na wiki (camada 3 > camada 2, fundamentos > ferramentas). Contribuição nova principal: taxonomia deep/shallow modules (Ousterhout) como affordance para IA, e operacionalização de guides com skills concretas (Grill Me, Ubiquitous Language, Improve Architecture). Cita Kent Beck diretamente.

## [2026-06-09] ingest | Memória de Agentes IA: Karpathy LLM Wiki e agentmemory na Prática
- Fonte: "Memória de Agentes IA: Karpathy LLM Wiki e agentmemory na Prática" por Fabio Akita, publicado em akitaonrails.com (2026-05-18)
- Páginas criadas: wiki/sources/memoria-agentes-karpathy-agentmemory, wiki/concepts/compaction-de-contexto, wiki/concepts/llm-wiki-karpathy, wiki/concepts/memoria-longo-prazo-agentes, wiki/entities/fabio-akita, wiki/entities/andrej-karpathy, wiki/entities/agentmemory
- Páginas atualizadas: wiki/entities/claude-code, wiki/entities/codex-openai, wiki/entities/opencode, index.md
- Observações: Artigo técnico denso com análise de código-fonte dos 3 agentes. Revela implementações internas de compaction (Claude Code tem 3 níveis, Codex faz handoff, opencode faz anchored summary). Apresenta padrão LLM Wiki do Karpathy como solução para memória de longo prazo. agentmemory é implementação MCP do padrão mas com problemas de maturidade (autor migrou para ai-memory em Rust após 1 semana).

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
