---
title: "Matt Pocock"
type: entity
tags: [pessoa, educador, typescript, ai-coding]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[wiki/sources/software-fundamentals-matter-more-than-ever]]", "[[wiki/sources/full-walkthrough-workflow-ai-coding]]"]
---

# Matt Pocock

## Quem é

Educador e desenvolvedor TypeScript. Criador do curso "Claude Code for Real Engineers" e do repositório `mattpocock/skills` (13k+ stars no GitHub). Publica conteúdo em YouTube e no site aihero.dev.

## Posição na era IA

Defende que fundamentos de engenharia de software são **mais** importantes na era da IA, não menos. Critica o movimento specs-to-code como "vibe coding por outro nome". Propõe um workflow baseado em:

1. Design concept compartilhado (interrogação exaustiva antes de gerar)
2. Linguagem ubíqua (DDD aplicado à comunicação humano-IA)
3. TDD para forçar small steps
4. Deep modules (Ousterhout) para navegabilidade
5. Design da interface com delegação da implementação

## Contribuições relevantes

- **Skill "Grill Me":** força a IA a interrogar o usuário até atingir entendimento compartilhado (22-100 perguntas)
- **Skill "Ubiquitous Language":** escaneia o codebase e gera markdown com terminologia alinhada
- **Skill "Improve Codebase Architecture":** reorganiza código em deep modules
- **Skill "Write a PRD":** transforma design concept em documento de destino (user stories + decisions)
- **Skill "PRD to Issues":** quebra PRD em vertical slices com blocking relationships (Kanban)
- **Sandcastle:** lib TypeScript para paralelizar agentes AFK em Docker (implementer/reviewer/merger)

## Workflow completo (workshop)

Demonstrado em workshop de 1h36min com codebase real:

1. **Grill Me** — alinhamento até shared design concept
2. **PRD** — sumarização do destino (não revisa: confia no alinhamento)
3. **Kanban Board** — DAG de tickets com vertical slices e blocking
4. **Ralph loop** — implementação AFK com TDD (Sonnet)
5. **Automated Review** — review em contexto limpo (Opus)
6. **QA humana** — imposição de taste, gera novos tickets

Usa modelos diferentes por fase: Sonnet para implementação, Opus para review.

## Ferramentas que usa

- [[wiki/entities/claude-code]] (ferramenta principal de coding com IA)

## Relação com outros autores

- Cita [[wiki/entities/kent-beck]] ("invest in the design of the system every day")
- Referencia John Ousterhout, Frederick Brooks, Eric Evans (DDD)
- Alinhamento com teses de [[wiki/entities/zarathon-viana]] (camada 3 > camada 2) e [[wiki/entities/birgitta-bockeler]] (harness como guides)

## Referências

- [[wiki/sources/software-fundamentals-matter-more-than-ever]]
- [[wiki/sources/full-walkthrough-workflow-ai-coding]]
- YouTube: Matt Pocock
- Site: aihero.dev
- GitHub: mattpocock/course-video-manager (744+ issues closed)
