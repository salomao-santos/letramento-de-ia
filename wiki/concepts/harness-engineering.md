---
title: "Harness Engineering"
type: concept
tags: [harness-engineering, agentes-ia, ferramentas]
created: 2026-06-08
updated: 2026-06-09
sources: ["[[wiki/sources/as-3-camadas-do-coding-com-ia]]", "[[wiki/sources/arquitetura-na-era-dos-agentes]]", "[[wiki/sources/engenharia-era-piloto-automatico]]", "[[wiki/sources/software-fundamentals-matter-more-than-ever]]", "[[wiki/sources/harness-beyond-skills-sensors]]", "[[wiki/sources/spec-driven-limite-harness-proximo-passo]]", "[[wiki/sources/voltei-do-vale-do-silicio-dev-2026]]", "[[wiki/sources/fluxo-completo-dev-avancado-ia]]", "[[wiki/sources/rules-skills-mcps-subagents-waldemar]]"]
---

# Harness Engineering

## Definição

"Harness" vem de arreio de cavalo (rédea, sela, freio, bridão). O modelo é o cavalo — potente, rápido, mas sem rumo. O harness é tudo que canaliza essa potência numa direção útil.

Fórmula canônica: **Agent = Model + Harness**

Definição aceita por [[wiki/entities/martin-fowler]], OpenAI, LangChain, Anthropic e Thoughtworks.

## Componentes do Harness

### Inner Harness (vem com a ferramenta)
- System prompt
- Mecanismo de retrieval
- Orquestração de tools

### Outer Harness (você constrói por cima)
- Contexto persistente: CLAUDE.md, AGENTS.md, .cursorrules
- Tools e MCPs
- Sub-agents
- Hooks
- Skills
- Sensores computacionais

### Outer Harness operacionalizado (Waldemar — demo completa)

[[wiki/sources/fluxo-completo-dev-avancado-ia]] detalha a implementação prática do outer harness num monorepo real:

| Camada | Papel | Exemplo |
|--------|-------|---------|
| Rules | Estrutura base + progressive disclosure | "Se envolve módulos → leia X" |
| Docs | Padrões específicos do projeto | architecture overview, coding patterns, migrations |
| Skills | Tática local reutilizável | Skill Confluence, Skill Jira |
| MCPs | Contexto remoto (API para LLMs) | Atlassian MCP, Context7 |

**Diferença-chave:** MCP busca conhecimento que está **em outro lugar** (Confluence, Jira). Skill é instrução **local** de como usar esse conhecimento. Docs são referência **persistente** do projeto.

**Investimento incremental:** "Cada vez que gero um plano que falta algo, melhoro a documentação até atingir o Nirvana." Levou dias para criar o contexto; o retorno é uma feature de 7 dias em 1 hora.

### Evolução do Outer Harness: Skills substituem Custom Sub Agents

[[wiki/sources/rules-skills-mcps-subagents-waldemar]] documenta a evolução histórica do outer harness:

**Antes (2024):** capabilities e isolamento de contexto estavam misturados em custom sub agents. Resultado: sub agents de 2000-4000 linhas que consumiam metade do contexto ao iniciar.

**Agora (2025):** separação clara em dois conceitos:

| Necessidade | Solução Antiga | Solução Atual |
|-------------|---------------|---------------|
| Habilidade específica (criar teste, buscar Jira) | Custom sub agent | **Skill** (~66 linhas, portável) |
| Processo isolado (paralelização, pesquisa pesada) | Custom sub agent | **Sub agent genérico** (Cursor/Claude Code nativo) |

**Progressive Disclosure** completa o quadro: em vez de carregar tudo na memória do agente ao iniciar, cada componente do harness (rules, skills, MCPs) carrega sob demanda. O agente descobre o que precisa e busca.

Mensagem consensual da indústria (Cursor, Anthropic, Claude Code): **"Foquem em criar skills, que a parte de agente a gente vai resolver."**

### Clarificação terminológica (Böckeler & Ford)

[[wiki/sources/harness-beyond-skills-sensors]]: o termo "harness" é usado em **dois bounded contexts** na literatura:

1. **Inner harness:** Claude Code/Cursor/Replit harnesseiam o **modelo** (Sonnet, Opus)
2. **Outer harness:** o programador harnesseia o **agente** (Claude Code, Cursor)

Chris Ford: "You can't put the harness on the inside of a dog." Ao ler sobre harness engineering, sempre checar qual é o referente.

## Distinção importante

[[wiki/entities/zarathon-viana]] argumenta que Harness Engineering na acepção da literatura (camada 2) é importante mas insuficiente. A camada que mais pesa é a engenharia de software clássica ([[wiki/concepts/tres-camadas-coding-ia]]).

## Harness como comunicação

Zarathon expande o conceito: harness não é só tooling, é também **comunicação**. A habilidade de se expressar com clareza, sem ambiguidade e de forma token-efficient é parte do harness. Quem não declara intenção de forma direta e pragmática perde tempo em pingpong com a LLM e polui o contexto.

> "Harness não é só tooling, harness também é comunicação."

## Design Concept e Ubiquitous Language como Guides (Matt Pocock)

[[wiki/entities/matt-pocock|Matt Pocock]] operacionaliza o conceito de guides com duas práticas:

1. **Design concept compartilhado:** interrogação exaustiva (skill "Grill Me") para alinhar visão antes de gerar código. É um guide de processo — canaliza a IA antes que ela escreva qualquer linha.
2. **Ubiquitous language:** arquivo markdown com terminologia do domínio, usado consistentemente em código, planejamento e conversas. É um guide persistente — a IA consulta a cada interação.

Ambos são feedforward puro: moldam o comportamento da IA antes da ação, exatamente como a taxonomia Böckeler/Fowler define "guides".

## Categorias (Fowler/Böckeler)

- **Guides (feedforward):** instruções que canalizam o comportamento do agente antes da ação
- **Sensors (feedback):** verificações que detectam problemas depois da ação ([[wiki/concepts/sensores-computacionais]])

### Analogia GPS ([[wiki/sources/spec-driven-limite-harness-proximo-passo]])

- **Feed forward** = a rota que o GPS traça antes de sair
- **Feedback** = GPS recalculando quando você erra a saída

Só rota → te perdes no primeiro erro. Só recálculo → sais sem direção. Precisa dos dois.

## Orquestração Multi-Agente

[[wiki/sources/spec-driven-limite-harness-proximo-passo]]: o caminho é ter agentes **em processos separados** com missões distintas — não sub-agents dentro do mesmo contexto:

- **Agente Build:** implementa (fará de tudo para cumprir, inclusive deletar código)
- **Agente QA:** valida contra um contrato concordado (rejeita o que não passa)
- **Orquestrador:** inicia ciclos Build → QA → Build até convergir

O mecanismo-chave é o **contrato**: lista concordada entre Build e QA antes da implementação. Sem contrato, QA sugere coisas não relacionadas e gera loop infinito.

Dado: código vazado do Claude Code já mostra instrumentação para essa orquestração nativa.

## Investimento contínuo no Harness

Insight do time OpenAI (Ryan LeCompte) e reforçado por Böckeler: equipes produtivas gastam a maior parte da energia **no harness**, não no código. Quase nunca tocam o código diretamente. Cada falha recorrente vira um novo sensor ou guide.

> O que distingue uso produtivo de vibe coding com entropia crescente é o reinvestimento contínuo no harness.

Paralelo com Kent Beck (via [[wiki/entities/matt-pocock]]): "Invest in the design of the system every day."

## Quem constrói o Harness: Product Engineer

[[wiki/concepts/product-engineer]]: o perfil em alta demanda em 2026, segundo relatos do Vale do Silício ([[wiki/sources/voltei-do-vale-do-silicio-dev-2026]]). O Product Engineer é definido como "quem constrói a coisa que constrói a coisa" — combinando senso de produto com construção de harness/infra de qualidade.

Exemplos concretos do Cursor:
- Code review automatizado por t-shirt size
- Specs estruturadas para agentes
- MCP central com governança
- Self healing (agente arruma PRs sozinho)
- Agentes que abrem PRs para melhorar código

> O Product Engineer constrói o outer harness para que builders (e agentes) entreguem em produção com segurança.

## Ver também

- [[wiki/concepts/tres-camadas-coding-ia]]
- [[wiki/concepts/ambient-affordances]]
- [[wiki/concepts/spec-driven-development]]
- [[wiki/concepts/sensores-computacionais]]
- [[wiki/concepts/product-engineer]] — quem constrói o harness na prática
- [[wiki/sources/harness-engineering-fowler]] — artigo fonte original
- [[wiki/sources/maintainability-sensors]] — aplicação prática dos sensores
- [[wiki/sources/harness-beyond-skills-sensors]] — deep dive em sensores com experimento
- [[wiki/sources/software-fundamentals-matter-more-than-ever]] — skills como guides práticos
- [[wiki/sources/spec-driven-limite-harness-proximo-passo]] — spec-driven como subset, multi-agente, 6 falhas
- [[wiki/sources/voltei-do-vale-do-silicio-dev-2026]] — Product Engineer como quem constrói o harness
