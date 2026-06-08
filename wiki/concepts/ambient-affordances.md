---
title: "Ambient Affordances"
type: concept
tags: [arquitetura, agentes-ia, estrutura-de-codigo]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[wiki/sources/arquitetura-na-era-dos-agentes]]"]
---

# Ambient Affordances

## Definição

Termo de Ned Letcher (Thoughtworks). São as propriedades estruturais do ambiente de código que o tornam legível, navegável e tratável por agentes de IA.

> "Não é só sobre as regras que você escreve. É sobre como o código tá organizado."

## Exemplos

- Estrutura de pastas por domínio (não por tipo)
- Convenções de nomenclatura consistentes
- Service templates com cercas pré-montadas
- Glossário de linguagem ubíqua no root do repo
- README de módulo com contratos e responsabilidades

## Service Templates

Quando um time tem um template padronizado para novo serviço (estrutura de pastas, CI configurado, linter, testes de arquitetura, documentação de domínio), o agente começa num ambiente com cercas já montadas.

## Organização por domínio vs por tipo

| Por domínio ✅ | Por tipo ❌ |
|---------------|-----------|
| `payments/` | `controllers/` |
| `contracts/` | `services/` |
| `notifications/` | `models/` |

Organização por domínio é infinitamente mais navegável para agentes. O contexto fica junto. A fronteira fica visível.

## Impacto

Times greenfield podem embutir harnessability desde o dia 1. As escolhas de tecnologia e arquitetura determinam o quão governável o código vai ser.

## Ver também

- [[wiki/concepts/harness-engineering]]
- [[wiki/concepts/sensores-computacionais]]
- [[wiki/sources/arquitetura-na-era-dos-agentes]]
