---
title: "Full Walkthrough: Workflow for AI Coding"
type: source
tags: [workflow, ai-coding, tdd, kanban, vertical-slices, smart-zone, compaction, parallelização, matt-pocock]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[raw/clippings/Full Walkthrough - Workflow for AI Coding — Matt Pocock]]"]
---

# Full Walkthrough: Workflow for AI Coding — Matt Pocock

## Metadados

- **Autor:** [[wiki/entities/matt-pocock|Matt Pocock]]
- **Tipo:** Workshop (conferência, hands-on)
- **Data:** 2025-06-09
- **URL:** https://www.youtube.com/watch?v=-QFHIoCo-Ko
- **Duração:** ~1h36min

## Tese central

> A IA não é um compilador de specs. É um colaborador com memória curta que precisa de alinhamento, feedback loops curtos e tarefas pequenas.

O workshop operacionaliza a filosofia da palestra "Software Fundamentals Matter More Than Ever" num workflow passo-a-passo: ideia → grill → PRD → Kanban → implementação AFK → QA humana.

## Conceitos-chave apresentados

### Smart Zone / Dumb Zone

LLMs têm um limiar de qualidade (~100K tokens) após o qual degradam. Relações de atenção escalam quadraticamente com cada token adicionado. Implicação: dimensionar tarefas para caber na smart zone.

Referência: conceito de Dex Hardy (Human Layer).

### Clear > Compact (Memento model)

Matt recomenda **limpar contexto e recomeçar** (como o protagonista de Memento) em vez de compactar. Justificativa: estado limpo é previsível e reprodutível; compaction cria "sedimentos" que degradam qualidade progressivamente.

> "Devs love compacting for some reason, but I hate it. I much prefer my AI to behave like the guy from Memento."

### Fases de uma sessão LLM

Toda sessão passa por: System Prompt → Exploração → Implementação → Testes. Ao limpar, volta ao system prompt (estado determinístico).

### Grill Me (demonstração prática)

Skill minimalista que força a IA a interrogar o usuário até atingir entendimento compartilhado. No workshop, gerou 22 perguntas antes de convergir. Design concept (Frederick Brooks) é o objetivo, não um artefato.

> "I didn't need a plan, I needed to be on the same wavelength as the AI."

### PRD como documento de destino

PRD documenta o destino (onde chegar); Kanban documenta a jornada (como chegar). Matt não revisa o PRD porque confia na capacidade de sumarização do LLM após alinhamento via grill. O valor está no alinhamento, não no documento.

### Kanban com blocking relationships (DAG)

Em vez de planos sequenciais (fases numeradas), criar tickets com dependências explícitas. Isso permite paralelização: múltiplos agentes podem trabalhar em tickets independentes simultaneamente.

### AFK tasks vs Human-in-the-loop

- **Human-in-the-loop:** planejamento, grilling, QA — exigem presença humana
- **AFK tasks:** implementação — podem rodar sem humano presente

Metáfora: day shift (planejamento) e night shift (implementação).

### Vertical slices / Tracer bullets

A IA naturalmente codifica horizontalmente (toda a DB → toda a API → todo o frontend). Isso é anti-padrão porque não produz feedback até a última fase.

Corrigir para vertical slices: cada ticket deve tocar todas as camadas (schema + service + UI mínima), gerando algo testável end-to-end.

Referência: *The Pragmatic Programmer* (tracer bullets), Martin Fowler (refactoring).

### Ralph loop

Loop de implementação AFK: script bash que alimenta o agente com issues do backlog, últimos 5 commits, e um prompt de implementação. O agente pega o próximo ticket, implementa com TDD, roda feedback loops (testes + types), e commita.

### TDD no Ralph loop

TDD é "absolutely essential" para AFK coding. Red-green-refactor força o agente a instrumentar o código antes de implementar, tornando mais difícil "colar" nos testes. Sem feedback loops, a IA "codes blind".

> "If your code base doesn't have feedback loops, you're never ever ever going to get decent output out of AI."

### Sandcastle (paralelização)

Ferramenta TypeScript criada por Matt para rodar loops AFK em paralelo:
1. **Planner** — analisa backlog, identifica tickets paralelizáveis
2. **Implementer** (Sonnet) — executa em Docker sandbox, um por ticket
3. **Reviewer** (Opus) — revisa commits em contexto limpo (smart zone)
4. **Merger** — resolve conflitos e merge

### Push vs Pull para coding standards

- **Implementer** acessa coding standards via **pull** (skills disponíveis para consulta)
- **Reviewer** recebe coding standards via **push** (instrução direta no prompt)

Lógica: o implementer precisa de liberdade; o reviewer precisa de rigor.

### Doc rot

PRDs e documentação de features desatualizam rapidamente. Matt recomenda fechar/descartar issues/PRDs após implementação para evitar que influenciem negativamente sessões futuras.

### QA como imposição de taste

QA manual é o momento de impor opinião humana sobre o código gerado. Sem isso, o output "lacks taste". Cada bug encontrado no QA gera novo ticket no Kanban.

### Deep modules + code review seletivo

O humano precisa conhecer as **interfaces** dos módulos, mas pode delegar a implementação interna. Deep modules como gray boxes permitem manter visão do codebase sem exaustão.

## Fluxo completo (resumo visual)

```
Ideia → Grill Me (human-in-the-loop)
  → PRD (destino, não reviso)
    → Kanban Board (vertical slices, DAG)
      → Ralph loop AFK (TDD, feedback loops)
        → Automated Review (contexto limpo)
          → QA humana (imposição de taste)
            → Code review (time)
```

## Ferramentas mencionadas

- [[wiki/entities/claude-code]] (ferramenta principal do workshop)
- Sandcastle (lib TypeScript para paralelização, autoria própria)
- Docker (sandbox para agentes AFK)
- GitHub Issues (backlog real do `mattpocock/course-video-manager`)
- Slido (Q&A do workshop)

## Livros referenciados

- *The Pragmatic Programmer* — Hunt & Thomas (tracer bullets, outrunning headlights)
- *The Design of Design* — Frederick P. Brooks (design concept)
- *A Philosophy of Software Design* — John Ousterhout (deep modules)
- *Refactoring* — Martin Fowler (keep tasks small)

## Relação com outros conceitos da wiki

- [[wiki/concepts/compaction-de-contexto]] — Matt propõe clear > compact
- [[wiki/concepts/tdd-como-especificacao]] — TDD como feedback loop essencial para AFK
- [[wiki/concepts/spec-driven-development]] — crítica reiterada: specs-to-code não funciona
- [[wiki/concepts/ambient-affordances]] — deep modules como estrutura que viabiliza o workflow
- [[wiki/concepts/harness-engineering]] — skills como guides, TDD como sensor, reviewer como harness
- [[wiki/concepts/tres-camadas-coding-ia]] — workflow inteiro é camada 3 (engenharia)
- [[wiki/concepts/automation-complacency]] — QA manual como antídoto

## Referências

- [[raw/clippings/Full Walkthrough - Workflow for AI Coding — Matt Pocock]]
- [[wiki/sources/software-fundamentals-matter-more-than-ever]] — palestra teórica complementar
- GitHub: mattpocock/course-video-manager (744+ issues closed)
