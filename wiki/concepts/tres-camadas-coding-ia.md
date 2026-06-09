---
title: "As 3 Camadas do Coding com IA"
type: concept
tags: [modelo-mental, coding-com-ia, harness-engineering]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[wiki/sources/as-3-camadas-do-coding-com-ia]]"]
---

# As 3 Camadas do Coding com IA

Modelo proposto por [[wiki/entities/zarathon-viana]] para organizar o pensamento sobre engenharia de software na era dos agentes de IA.

## As Camadas

| Camada | O que é | Controle | O que você faz |
|--------|---------|----------|----------------|
| 1. Modelo | O LLM em si | Baixo | Escolhe |
| 2. Ferramenta | O harness (Claude Code, Cursor, etc.) | Médio | Configura e estende |
| 3. Engenharia de Software | Práticas clássicas (TDD, arquitetura, CI/CD) | Alto | Escreve, define, audita |

## Insight Central

> "Quanto mais próximo do modelo, menos controle você tem. Quanto mais próximo da engenharia de software clássica, mais controle você tem."

## Por que importa

A maioria do tempo e energia da comunidade está na camada 2 (MCPs, sub-agents, context engineering). Mas a camada 3 oferece **mais alavanca por hora investida**:

- Um dia estudando AGENTS.md → ganho moderado
- Um dia escrevendo suíte de testes sólida → ganho muito maior (vira cerca para qualquer LLM futuro)

A camada 3 é **investment capital**. As outras são **running cost**.

## Pilares da Camada 3

1. **Arquitetura** → define POR ONDE o agente pode ir ([[wiki/sources/arquitetura-na-era-dos-agentes]])
2. **Testes** → define O QUE o agente deve produzir ([[wiki/sources/tdd-na-era-dos-agentes]])
3. **Code Review** → define SE pode passar ([[wiki/sources/code-review-na-era-dos-agentes]])

## Ver também

- [[wiki/concepts/harness-engineering]]
- [[wiki/concepts/sensores-computacionais]]
