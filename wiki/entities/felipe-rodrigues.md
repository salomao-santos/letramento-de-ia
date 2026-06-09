---
title: "Felipe Rodrigues"
type: entity
tags: [pessoa, autor, tech-leads-clube, brasil, skills]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[wiki/sources/rules-skills-mcps-subagents-waldemar]]"]
---

# Felipe Rodrigues

## Quem é

Membro e co-host do **Tech Leads Clube** (@techleadsclub). Participa das lives com [[wiki/entities/waldemar-neto|Waldemar Neto]], trazendo demonstrações práticas e experiências pessoais com agentes de IA.

## Contribuição principal

- Criador da skill **TLC Spec Driven** (skill do Tech Leads Clube para spec-driven development)
- Demonstrou a migração prática de um sub agent customizado (~2000 linhas) para múltiplas skills compactas (~66 linhas cada)
- Criou skills especializadas: core standards, create component, form, integrate API

## Posições-chave

- Sub agents grandes consumiam metade do contexto ao iniciar — inviável no plano mais barato do Claude
- Skills com front matter descritivo fazem o agente invocar automaticamente (sem precisar dizer "usa a skill X")
- "Dá para fazer skill de qualquer coisa": slides, PDFs, RFCs, design docs, formulários complexos
- Recomenda symlink para instalação de skills (auto-atualização quando a lib é atualizada)
- Contribuiu com a biblioteca de skills curadas do Tech Leads Clube

## Práticas demonstradas

- Skill com max 66 linhas + front matter com `description` para invocação automática
- Exemplos: "use when task mentions schemas validation field arrays disabled states"
- Skills instaláveis via CLI com detecção automática de IDEs

## Publicações nesta wiki

- [[wiki/sources/rules-skills-mcps-subagents-waldemar]]
- [[wiki/sources/spec-driven-guia-completo-waldemar]] (mencionado como criador da skill TLC Spec Driven)

## Links

- Tech Leads Clube (Circle community)
