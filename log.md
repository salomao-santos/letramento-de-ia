---
title: "Log de Operações"
type: log
created: 2026-06-08
updated: 2026-06-09
---

# Log de Operações

## [2026-06-09] ingest | Rules, Skills, MCPs e Subagents — DOMINE os principais conceitos (Waldemar Neto & Felipe Rodrigues)
- Fonte: "Rules, Skills, MCPs e Subagents - DOMINE os principais conceitos de IA para ganhar PRODUTIVIDADE" por Waldemar Neto e Felipe Rodrigues (Tech Leads Clube), YouTube (2025-02-07), ~45min
- Páginas criadas: wiki/sources/rules-skills-mcps-subagents-waldemar, wiki/entities/felipe-rodrigues
- Páginas atualizadas: wiki/entities/waldemar-neto (novas posições-chave), wiki/concepts/compaction-de-contexto (progressive disclosure, regra 40%), wiki/concepts/harness-engineering (evolução skills vs sub agents, progressive disclosure), index.md
- Observações: Aula que documenta a morte dos custom sub agents em favor de skills + sub agents genéricos. Contribuições novas: progressive disclosure como padrão formal (IA descobre e carrega sob demanda), regra 40% (complementa 30% como meta), taxonomia Agent (papel) vs Skill (habilidade), caso concreto de migração sub agent 2000 linhas → skills 66 linhas, marketplace de skills versionadas como padrão enterprise, biblioteca open-source de skills curadas do Tech Leads Clube. Felipe Rodrigues aparece como co-host com contribuições práticas relevantes.

## [2026-06-09] ingest | Meu fluxo COMPLETO de desenvolvimento avançado com IA (Waldemar Neto)
- Fonte: "Meu fluxo COMPLETO de desenvolvimento avançado com IA" por Waldemar Neto (Tech Leads Clube), YouTube (2025-01-25), ~22min
- Páginas criadas: wiki/sources/fluxo-completo-dev-avancado-ia
- Páginas atualizadas: wiki/entities/waldemar-neto (novas posições-chave, nova fonte), wiki/concepts/harness-engineering (outer harness operacionalizado com tabela rules/docs/skills/MCPs), wiki/concepts/compaction-de-contexto (regra 30%, delegação de plano), wiki/concepts/spec-driven-development (demonstração end-to-end do RPI, cross-ref), index.md
- Observações: Vídeo prático demonstrando RPI end-to-end com integração Stripe em monorepo. Contribuições novas: regra 30% da janela de contexto como meta operacional, padrão de delegação modelo caro→barato para plan→implement, Git worktrees como vetor de paralelização (2-3 agentes simultâneos), diferença clara MCP vs Skill vs Docs, documentação incremental como investimento até "Nirvana". Complementa diretamente o guia teórico anterior (spec-driven-guia-completo-waldemar).

## [2026-06-09] ingest | Clean Architecture está te CUSTANDO CARO na era da IA (Waldemar Neto)
- Fonte: "Clean Architecture está te CUSTANDO CARO na era da IA" por Waldemar Neto (Tech Leads Clube), YouTube (2025-06-26), ~16min
- Páginas criadas: wiki/sources/clean-architecture-custando-caro-era-ia, wiki/concepts/custo-abstracoes-era-ia
- Páginas atualizadas: wiki/entities/waldemar-neto (novas posições-chave, nova fonte), wiki/concepts/ambient-affordances (dados Navigation Paradox, nova fonte), wiki/concepts/sensores-computacionais (cross-ref, alternativa barata a Clean Architecture), index.md
- Observações: Vídeo que questiona implementação ritualística de Clean Architecture na era dos agentes. Contribuições novas: paper Navigation Paradox (2026) com dados quantitativos (76% acurácia, 58% ignore de ferramentas), conceitos "abstraction bloat" (Addy Osmani) e "abstraction illusion" (Super Productivity), distinção clara encapsulamento vs inversão de dependência, regra "estratégico primeiro, flat depois, abstrai por dor", YAGNI escalado pela IA. Reforça fortemente: DDD estratégico como otimização de contexto, organização por domínio, deep modules, testes de comportamento e lint rules como alternativa barata a camadas arquiteturais.

## [2026-06-09] ingest | Voltei do Vale do Silício: Esse é o Dev que QUEREM em 2026 (Waldemar Neto)
- Fonte: "Voltei do Vale do Silício: Esse é o Dev que QUEREM em 2026" por Waldemar Neto (Tech Leads Clube), YouTube (2025-06-09), ~16min
- Páginas criadas: wiki/sources/voltei-do-vale-do-silicio-dev-2026, wiki/concepts/product-engineer
- Páginas atualizadas: wiki/entities/waldemar-neto (nova fonte, posições-chave do Vale), wiki/entities/cursor (práticas internas, Canvas, 40-50% não-devs, cloud agents), wiki/concepts/harness-engineering (seção Product Engineer como quem constrói o harness), index.md
- Observações: Vídeo com relatos de primeira mão após visita ao Vale do Silício (Cursor, Try, Stripe, Databricks). Contribuição nova principal: conceito de Product Engineer com duas faces (senso de produto + harness/qualidade), "taste" como skill, 4 histórias concretas (orquestração entre reuniões, 5 cloud agents paralelos, dados de produção via MCP antes de codar, Canvas para investigação de incidentes), gap Brasil × Vale como oportunidade, 4 movimentos práticos. Reforça fortemente: harness engineering, código como uma das skills (não a principal), autonomia e contexto de negócio como alavanca.

## [2026-06-09] ingest | Spec-Driven Development: A Habilidade #1 para Devs de 2026 (Guia Completo) (Waldemar Neto)
- Fonte: "Spec-Driven Development: A Habilidade #1 para Devs de 2026 (Guia Completo)" por Waldemar Neto (Tech Leads Clube), YouTube (2025-05-01), ~12min
- Páginas criadas: wiki/sources/spec-driven-guia-completo-waldemar, wiki/entities/waldemar-neto
- Páginas atualizadas: wiki/concepts/spec-driven-development (seção operacionalização prática com RPI e subagents), wiki/concepts/compaction-de-contexto (RPI como implementação de Clear > Compact), wiki/sources/spec-driven-limite-harness-proximo-passo (autor corrigido para Waldemar), wiki/entities/zarathon-viana (removidas fontes incorretamente atribuídas), index.md
- Observações: Vídeo tutorial/operacional que complementa o outro vídeo crítico do mesmo autor. Correção de atribuição: ambos os vídeos do Tech Leads Clube (este e "Spec Driven chegou no limite") são do Waldemar Neto, não do Zarathon Viana. Contribuições novas: framework RPI (Research → Plan → Implement), caso real 90 arquivos/50K tokens, subagents para paralelização (4 simultâneos), conceito de "estado" como memória de decisões, skill TLC Spec Driven (Felipe Rodrigues).

## [2026-06-09] ingest | Spec Driven chegou no limite — Harness Engineering é o próximo passo (Waldemar Neto)
- Fonte: "Spec Driven chegou no limite — Harness Engineering é o próximo passo" por Waldemar Neto (Tech Leads Club), YouTube (2025-06-09), ~12min
- Páginas criadas: wiki/sources/spec-driven-limite-harness-proximo-passo
- Páginas atualizadas: wiki/concepts/harness-engineering (orquestração multi-agente, analogia GPS, contrato Build↔QA), wiki/concepts/spec-driven-development (tabela 6 falhas, limitações explícitas), wiki/concepts/sensores-computacionais (agente não deve julgar — 0/1), wiki/concepts/memoria-longo-prazo-agentes (amnésia como falha #3), wiki/entities/waldemar-neto (posições-chave, nova fonte), index.md
- Observações: Vídeo que posiciona spec-driven explicitamente como subset de harness (cobre 2 de 6 falhas). Contribuições novas: tabela de 6 falhas com score, analogia GPS (feed forward = rota, feedback = recálculo), mecanismo de contrato para orquestração multi-agente (evita loop infinito), framework PBQ como implementação prática (51¢ para todo-list completa com QA loop), referência a código vazado do Claude Code mostrando instrumentação multi-agente. Reforça fortemente: sensores > instrução, agente como self-judge é anti-padrão, slope acumulado em sistemas grandes.

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
