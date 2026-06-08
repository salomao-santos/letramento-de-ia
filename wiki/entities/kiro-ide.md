---
title: "Kiro"
type: entity
tags: [ferramenta, ide, aws, spec-driven-development]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[wiki/sources/spec-driven-development]]"]
---

# Kiro

## O que é

IDE baseada em VS Code, desenvolvida pela AWS. Implementa uma abordagem de Spec-Driven Development com workflow guiado de Requirements → Design → Tasks.

## Workflow

1. **Requirements** — User Stories no formato "As a..." com acceptance criteria (GIVEN/WHEN/THEN)
2. **Design** — Documento com arquitetura de componentes, data flow, modelos, error handling, testing strategy
3. **Tasks** — Lista de tarefas rastreáveis aos requirements, com UI para execução uma a uma

## Conceitos

- **Steering** (memory bank) — Arquivos de contexto persistente (.kiro/steering/)
- **Specs** — Artefatos por feature (requirements.md, design.md, tasks.md)
- **Hooks** — Automações baseadas em eventos da IDE

## Avaliação (Böckeler)

- Mais leve das ferramentas SDD analisadas
- Workflow intuitivo (3 arquivos apenas)
- Porém: para bugs pequenos, gera overhead desproporcional ("sledgehammer to crack a nut")
- Atualmente mais spec-first do que spec-anchored

## Ver também

- [[wiki/sources/spec-driven-development]]
- [[wiki/concepts/harness-engineering]]

## Links

- Site: https://kiro.dev/
