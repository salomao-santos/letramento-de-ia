---
title: "Voltei do Vale do Silício: Esse é o Dev que QUEREM em 2026"
type: source
tags: [product-engineer, vale-do-silicio, cursor, databricks, harness-engineering, builders]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[raw/clippings/Voltei do Vale do Silício - Esse é o Dev que QUEREM em 2026]]"]
---

# Voltei do Vale do Silício: Esse é o Dev que QUEREM em 2026

## Metadados

- **Autor:** [[wiki/entities/waldemar-neto|Waldemar Neto]] (Tech Leads Clube)
- **Formato:** Vídeo YouTube (~16min)
- **Data:** 2025-06-09
- **URL:** https://www.youtube.com/watch?v=iLyo0J8PRIA

## Resumo

Waldemar Neto volta de uma viagem ao Vale do Silício onde conversou com equipes do [[wiki/entities/cursor|Cursor]], Try, Stripe e Databricks. O vídeo apresenta o conceito de **Product Engineer** como o perfil de dev em alta demanda em 2026 — alguém que "constrói a coisa que constrói a coisa". Combina senso de produto (taste, analytics, autonomia de PM) com construção de harness/infra de qualidade que permite builders entregarem em produção com segurança.

## Teses principais

### 1. Democratização do software

- 40-50% dos usuários do Cursor **não são devs** (designers, founders, PMs, marketing)
- Try foca em "builders", não apenas devs
- Não é o fim dos devs — é **overlap crescente** entre builders e devs
- Quanto mais infraestrutura os devs provêm, mais coisas os builders conseguem fazer

### 2. O dev profissional no Vale virou orquestrador

- Ferramentas não são decisão consciente, são infraestrutura
- A engenheira do Cursor passa boa parte do dia em **analytics**, não código
- MCPs trazem contexto vivo do negócio (Linear, dashboards de produto)
- Boa parte do dia é conversar com PM e designer — juntar contexto
- Cursor cresceu sem manager tradicional — autonomia total para priorizar backlog
- Perfil esperado: orquestrador, validador, com autonomia de PM, taste de designer, fluência em analytics, e código como **uma** das skills

### 3. Taste

Capacidade de fazer julgamento estético e de qualidade sobre produto, código e design, **sem precisar de uma regra ou demanda explícita**. Mencionado em praticamente todas as empresas que visitou.

### 4. A alavanca > a IA

- IA acelera quem já tem alavanca
- Quem só recebe ticket vai entregar código mais rápido, mas está no mesmo lugar
- Quem tem contexto e autonomia trabalha em **escopo de produto**, não de ticket
- Construir alavanca virou a habilidade #1 em 2026
- Não depende de mudar de empresa — depende de ações práticas esta semana

### 5. Product Engineer = "constrói a coisa que constrói a coisa"

Conceito central. Duas faces inseparáveis:

| Face | O que é | Sem a outra vira... |
|------|---------|---------------------|
| Senso de produto | Decide o que construir, fala com PM, mede impacto, tem taste | PM disfarçado |
| Harness e qualidade | Constrói infra que permite builders entregarem rápido sem quebrar produção | Platform engineer com outro nome |

Empresas que contratam esse perfil: Stripe, Linear, Vercel.

## 4 histórias do Vale

### História 1 — Tech Lead do Databricks: orquestração entre reuniões

- Manhã cheia de reuniões (não mudou)
- No intervalo: dispara 2-3 cloud agents para avançar tasks
- Volta da reunião: revisa PRs dos agentes, dispara novos
- Ao longo do dia: 3-4 PRs
- Dia virou **orquestração e review**
- Tempo entre reuniões: antes perdido, agora onde mais código avança

### História 2 — Cursor: projetos longos viram trabalho de agente

- Projeto de meses quebrado em partes (feature full stack: schema → service → API → UI)
- Critério de quebra: "menor quantidade de trabalho + maior que um agente consegue fazer sem esbarrar em outro"
- Cada feature dispara ~5 cloud agents simultâneos
- Coordenação entre devs virou **coordenação entre agentes**
- Humano revisa código com ajuda de outro agente de code review
- Fluxo: 5 agentes implementando + 1 agente reviewer + engenheira validando

### História 3 — Cursor: dados antes de codar

- Antes de implementar, pede pro agente consultar banco de produção via MCP
- "Para essa feature de listagem, quantos usuários teriam mais de X itens?"
- Decisão de arquitetura sai **informada**, não chutada
- Agente conecta: feedback de usuário, dados de produção, métricas, audit logs
- **Agente vira pesquisador, dev vira decisor**

### História 4 — Cursor: investigação de incidente com Canvas

- Bug crítico em produção
- Engenheira abre Canvas (feature nova do Cursor) + único prompt
- Prompt: "Consulta Datadog, Audit Logs, cria timeline conectando ao histórico de PRs"
- Resultado: diagrama pronto, causa raiz identificada em minutos (PR mergeado antes do bug)
- Antes: dia inteiro em Confluence + Illustrator + múltiplas abas
- Agora: investigação + post mortem em minutos
- **Não é código mais rápido — é investigação, decisão e comunicação mais rápida**

## 4 movimentos práticos

1. **Mentalidade de produto:** ler "Product Minded Engineer" e "Extreme Programming Explained"
2. **Reunião com PM:** perguntar "qual métrica de negócio o time move este trimestre? Como minhas features se conectam?"
3. **Construir uma peça de harness:** template de spec, skill de code review, skill de testes
4. **Fundamentos de system design:** Designing Data-Intensive Applications, ByteByteGo, exercício semanal

> Nenhum desses movimentos é construir agentes ou aprender ML. Os quatro te aproximam do perfil de Product Engineer.

## Conexões com a wiki

- [[wiki/concepts/harness-engineering]] — Product Engineer constrói o harness para builders
- [[wiki/concepts/tres-camadas-coding-ia]] — Product Engineer opera na camada 3 (engenharia) para escalar camada 2
- [[wiki/concepts/spec-driven-development]] — Specs como peça de harness (exemplo de movimento 3)
- [[wiki/concepts/code-review-como-portao]] — Code review automatizado por t-shirt size no Cursor
- [[wiki/concepts/automation-complacency]] — Taste como antídoto (julgamento sem regra explícita)

## Referências

- [[raw/clippings/Voltei do Vale do Silício - Esse é o Dev que QUEREM em 2026]]
