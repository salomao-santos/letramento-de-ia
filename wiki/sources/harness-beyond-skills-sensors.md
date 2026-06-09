---
title: "Harness Engineering Beyond Skills: Using Sensors to Keep Your Coding Agent in Check"
type: source
tags: [sensores-computacionais, harness-engineering, mutation-testing, dependency-cruiser, experimento, linting]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[raw/clippings/Harness engineering beyond skills - Using sensors to keep your coding agent in check]]"]
---

# Harness Engineering Beyond Skills — Böckeler & Ford

## Metadados

- **Autores:** [[wiki/entities/birgitta-bockeler|Birgitta Böckeler]], Chris Ford
- **Tipo:** Vídeo/conversa (deep dive)
- **Data:** 2026-06-08
- **URL:** https://www.youtube.com/watch?v=uLWOLmeHOSE
- **Duração:** ~56 min
- **Relação:** Complementa [[wiki/sources/maintainability-sensors]] (artigo escrito). Este vídeo é a versão expandida com experimentos ao vivo e diálogo.

## Tese central

Sensores computacionais (feedback determinístico) são a parte mais subutilizada do harness engineering. O investimento contínuo no harness — e não no código diretamente — é o que distingue uso produtivo de "vibe coding com entropia crescente".

## Clarificação terminológica: inner vs outer harness

```
┌─────────────────────────────────────────────┐
│           Outer Harness (azul)              │  ← O que VOCÊ constrói
│  agents.md, tools, MCPs, hooks, sensores    │
│  ┌───────────────────────────────────┐      │
│  │       Inner Harness (roxo)        │      │  ← Claude Code, Cursor, etc.
│  │  system prompt, retrieval, tools  │      │
│  │  ┌───────────────────────┐        │      │
│  │  │       Modelo          │        │      │  ← Sonnet, Opus, etc.
│  │  └───────────────────────┘        │      │
│  └───────────────────────────────────┘      │
└─────────────────────────────────────────────┘
```

- **Inner harness** = o agente harnesseando o modelo (Claude Code harnesses Sonnet)
- **Outer harness** = o programador harnesseando o agente (você harnesses Claude Code)

Chris Ford: "You can't put the harness on the inside of a dog." O termo é usado em ambos os contextos na literatura; precisa sempre checar qual é o referente.

## Matriz guides × sensors (expandida)

|  | Feedforward (guides) | Feedback (sensors) |
|--|---------------------|-------------------|
| **Inferencial (GPU)** | Skills, agents.md, conventions | Review agents, AI modularity review |
| **Computacional (CPU)** | Code mods, language server, CLIs | Linter, type checker, mutation testing, dependency-cruiser |

Insight-chave: o foco atual da comunidade está nos **guides inferenciais** (a "batalha dos markdown files"). Os **sensors computacionais** estão subutilizados e oferecem confiabilidade superior.

## Experimento: com sensores vs sem sensores

### Setup
- App: dashboard de dados (Next.js/TypeScript), 4 APIs externas
- Modelo: Haiku (propositalmente fraco para provocar falhas)
- IDE: Cursor com sensor sidecar rodando em paralelo
- Feature: implementação de funcionalidade completa, partindo de "clean bill of health"

### Resultados sem sensores
- Estrutura de pastas: nomes e organização diferentes do padrão definido
- ESLint: `no-explicit-any` em excesso, imports não usados
- Test coverage: **caiu 6 pontos percentuais** (de 64% para ~58%)
- Lint errors: aumentaram
- TDD theater: agente criava teste "primeiro" mas só rodava 2 min depois
- Erros de error handling e problemas com `undefined` values

### Resultados com sensores
- Tudo verde no final (esperado — o agente tinha feedback para se corrigir)
- Agente corrigiu violações de cyclomatic complexity durante a sessão
- Dependency cruiser flagrou violações de camada → agente corrigiu
- Coverage subiu conforme sensores exigiram

### Conclusão do experimento
Sensores não apenas melhoram o resultado final — eles **direcionam a atenção do review humano**. O que não passou pelo sensor é o que merece olhar atento.

## Sensor sidecar — conceito de tooling

Böckeler vibe-codou uma ferramenta que:
1. Roda sensores em paralelo ao agente, em intervalo configurável
2. Tem **view humana** (dashboard visual com status verde/vermelho)
3. Tem **view otimizada para agente** (só mostra failures + custom messages para correção)
4. Registra checkpoints para análise post-mortem

O agente invoca um comando e recebe apenas os problemas com "positive prompt injection" — mensagens customizadas dizendo como abordar a correção.

## Agente modificando seus próprios sensores

Exemplo: regra `max-lines` com custom message:

> "Isso pode ser um design smell. Considere splittar. Mas se for um julgamento consciente e só 10 linhas acima do threshold, você pode aumentar levemente o threshold no config para este arquivo específico."

O agente aumentou de 500 → 550 linhas para um arquivo mock — não suprime globalmente, mas permite crescimento controlado. Se o arquivo crescer de novo, o sensor dispara novamente.

Isso é **self-modification controlada**: o agente adapta o harness, mas dentro de limites definidos pelo humano.

## Balanceamento guides vs sensors

Questão em aberto levantada:

1. Se sensores bons cobrem 40% dos casos que um guide tentava prevenir, o guide pode ser deletado?
2. Sensores permitem uso de modelos mais fracos (baratos) com resultados aceitáveis?
3. "Guide debt" existe — muitos markdowns que ninguém sabe se ajudam ou atrapalham

Chris Ford: "É superstição — uma vez pareceu funcionar, mas talvez fosse coincidência, talvez fosse outro modelo."

## Harness templates (especulação)

Ideia: templates pré-configurados por tipo de projeto:

| Template | Sensores típicos |
|----------|-----------------|
| Data dashboard | Structure rules, API client isolation, coverage gates |
| CRUD + relational DB | Entity integrity, migration safety, API linting |
| Event processing | Idempotency checks, schema validation, dead letter monitoring |

Uma skill instanciaria o template e configuraria todos os sensores na codebase nova automaticamente.

## Renaissance da static analysis

Chris Ford: "Mutation testing, property testing, fuzz testing — ouvi talks sobre isso por anos mas nunca implementei pela fricção. Agora posso pedir ao agente para configurar."

Böckeler: organizações têm SonarQube configurado que junta poeira. Agentes dão nova vida a essas ferramentas porque:
- Consomem o output automaticamente
- Corrigem issues sem intervenção humana
- O custo humano de "manter a casa limpa" caiu drasticamente

## Risco: ilusão de qualidade

> "Will this just give us an illusion of quality?"

Sensores verdes ≠ software correto. O risco de [[wiki/concepts/automation-complacency|automation complacency]] existe. Analogia: "Seatbelts might make people drive faster — but I'm still glad to have seatbelts."

## Relação com outros conceitos da wiki

- [[wiki/concepts/harness-engineering]] — este vídeo é o deep dive na metade "sensors" da taxonomia
- [[wiki/concepts/sensores-computacionais]] — validação prática extensiva
- [[wiki/concepts/mutation-testing]] — confirmado como crucial mas caro; runs incrementais
- [[wiki/concepts/automation-complacency]] — risco explicitamente levantado
- [[wiki/concepts/ambient-affordances]] — modularidade boa = boa para humanos E agentes
- [[wiki/sources/maintainability-sensors]] — artigo escrito; este vídeo é a versão expandida

## Referências

- [[raw/clippings/Harness engineering beyond skills - Using sensors to keep your coding agent in check]]
- Ryan LeCompte (OpenAI): artigo sobre harness engineering + "garbage collection" contínua
- [[wiki/sources/harness-engineering-fowler]] — artigo fundacional
- [[wiki/sources/maintainability-sensors]] — versão escrita deste conteúdo
