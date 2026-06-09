---
title: "Spec Driven chegou no limite — Harness Engineering é o próximo passo"
type: source
tags: [harness-engineering, spec-driven-development, sensores-computacionais, orquestracao-agentes, feed-forward, feedback]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[raw/clippings/Spec Driven chegou no limite — Harness Engineering é o próximo passo]]"]
---

# Spec Driven chegou no limite — Harness Engineering é o próximo passo

## Metadados

- **Autor:** [[wiki/entities/waldemar-neto|Waldemar Neto]] (Tech Leads Club)
- **Tipo:** Vídeo (YouTube)
- **Data:** 2025-06-09
- **URL:** https://www.youtube.com/watch?v=dLs-Pbn8stU
- **Duração:** ~12 min
- **Relação:** Continuação direta de [[wiki/sources/as-3-camadas-do-coding-com-ia]] e aplicação prática dos conceitos de [[wiki/sources/harness-engineering-fowler]]. Complementa [[wiki/sources/harness-beyond-skills-sensors]].

## Tese central

Spec Driven Development é um **subconjunto** de Harness Engineering — cobre o feed forward (guias preventivos), mas não cobre o feedback (sensores), memória entre sessões, nem orquestração multi-agente. Para escalar de "funcionalidades com IA" para "sistemas inteiros com IA", o próximo passo é harness completo.

## Definição de Harness (reforço)

O modelo é o engenheiro brilhante recém-contratado. O harness é o onboarding:
- Instruções, estrutura do repositório, linters, testes, arquivos de progresso, scripts de setup
- O gargalo não é mais a inteligência do modelo — é a qualidade do ambiente onde ele opera

O conceito explodiu em fevereiro de 2026 com posts da OpenAI, Anthropic e blog do Martin Fowler.

## 6 tipos de falha de agentes sem harness (Anthropic)

| # | Nome | Descrição | Spec Driven resolve? |
|---|------|-----------|---------------------|
| 1 | One Shot Hero | Tenta implementar tudo de uma vez, estoura contexto | ✅ Sim — quebra em tasks |
| 2 | Vitória prematura | Declara "pronto" sem terminar | ✅ Sim — define "done" explícito |
| 3 | Amnésia entre sessões | Sem memória do que veio antes | ❌ Parcial — não guarda estado |
| 4 | Validação superficial | Marca feature pronta sem testar de verdade | ❌ Depende — nem todo framework enforça |
| 5 | Processo único (self-judge) | Mesmo agente implementa e julga | ❌ Não — spec é single-process |
| 6 | Slope acumulado | Cada sessão piora 5%+, código degrada | ❌ Não — spec não enforça qualidade contínua |

Score: spec driven cobre 2 de 6 falhas completamente. As 4 restantes exigem harness completo.

## Framework conceitual: Feed Forward vs Feedback

Conceitos da **engenharia de controle** aplicados a agentes:

### Feed Forward (preventivo)
- Specs, agents.md, regras de arquitetura, skills
- Diz o que fazer **antes** da execução
- Analogia: a rota que o GPS traça antes de sair

### Feedback (corretivo)
- Linters, testes, type checkers, review agents
- Detecta erros **depois** da execução e permite autocorreção
- Analogia: GPS recalculando quando você erra a saída

> "A spec é feed forward puro. Ela diz o que fazer, mas não verifica se foi feito de forma certa."

Precisa dos dois: só rota = te perdes no primeiro erro. Só recálculo = sais sem direção.

## Orquestração multi-agente (separação de missões)

Insight central: o agente não deve ser quem julga seu próprio trabalho. A arquitetura proposta:

```
┌─────────────────────────────────┐
│         Orquestrador            │
├────────────────┬────────────────┤
│  Agente Build  │  Agente QA     │
│  (implementa)  │  (valida)      │
└────────────────┴────────────────┘
```

- São **processos separados**, não sub-agents dentro do mesmo contexto
- Agente Build: criará qualquer coisa para cumprir sua missão (inclusive deletar código)
- Agente QA: baterá item a item contra um contrato e rejeitará o que não passa
- Loop: QA rejeita → Build corrige → QA reavalia → até passar

**Contrato:** lista concordada entre Build e QA antes da implementação. Sem contrato, QA sugere coisas não relacionadas → loop infinito.

Dado concreto: código vazado do Claude Code já mostra instrumentação para essa orquestração.

## Demonstração prática: framework PBQ

Framework experimental baseado nos blog posts das empresas:
- Construído em cima de TLC Spec Driven (skill do Tech Leads Club)
- Adiciona: progress files, contratos, sprints, agente QA separado

### Fluxo
1. **Spec** → user stories, tasks
2. **Sprints** → agrupam tasks
3. **Progress file** → estado entre sprints (memória)
4. **Contrato** → Build e QA concordam no que será feito
5. **Build** → agente implementa
6. **QA (evaluation)** → outro agente valida contra contrato
7. **Loop** → se não passa, volta ao Build

### Resultado observado
- 51 centavos para implementação completa de todo-list
- Evaluation com score e threshold mínimo por critério
- Evaluation pode ser: testes unitários, integração, Playwright, etc.

## Custo (tokens)

"Vai gastar mais tokens? Certamente." — não há como fugir. É o custo de ter qualidade. Comparado com code review manual, refactoring depois, debugging — compensa.

## Ferramenta mencionada: get-done

Framework para Claude que implementa orquestração multi-agente com padrão similar. Ainda não estável, mas acompanhar a tendência.

## Contribuições novas (não presentes em outras fontes da wiki)

1. **Tabela de 6 falhas com score spec-driven** — primeira categorização explícita do que spec cobre vs não cobre
2. **Analogia GPS** (feed forward = rota, feedback = recálculo) — didática excelente
3. **Contrato Build↔QA** — mecanismo para evitar loop infinito entre agentes
4. **Framework PBQ** — implementação prática de harness sobre spec driven
5. **Custo real:** 51 centavos para app completa com QA loop
6. **Referência ao código vazado do Claude Code** — confirmação de que multi-agente está vindo nativamente

## Relação com outros conceitos da wiki

- [[wiki/concepts/harness-engineering]] — posiciona spec-driven como subset, não substituto
- [[wiki/concepts/spec-driven-development]] — análise explícita de limitações
- [[wiki/concepts/sensores-computacionais]] — sensores como o que "força" (retorna 0/1)
- [[wiki/concepts/memoria-longo-prazo-agentes]] — amnésia como falha #3
- [[wiki/concepts/tdd-como-especificacao]] — sensores > instrução para validação

## Referências

- [[raw/clippings/Spec Driven chegou no limite — Harness Engineering é o próximo passo]]
- Blog posts OpenAI e Anthropic sobre harness (fev 2026)
- [[wiki/sources/harness-engineering-fowler]]
- [[wiki/sources/harness-beyond-skills-sensors]]
- [[wiki/entities/waldemar-neto]]
