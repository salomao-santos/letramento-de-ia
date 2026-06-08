---
title: "TDD como Especificação"
type: concept
tags: [tdd, testes, especificação, coding-com-ia]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[wiki/sources/tdd-na-era-dos-agentes]]"]
---

# TDD como Especificação

## Shift mental

Na programação clássica, teste era safety net (verificação). Na era dos agentes, teste é **especificação** — o contrato determinístico que diz ao agente o que "funcionar" significa.

## Por que agora

O custo de escrever código caiu pra quase zero (agente gera em segundos). O que ficou caro foi **especificar a intenção**. Teste é a forma mais precisa e determinística de especificar intenção para uma máquina.

## O ciclo com agente

```
Humano escreve teste (RED) → Agente implementa (GREEN) → Colaboração refatora (REFACTOR)
```

**Regra de ouro:** nunca delegar o RED pro agente. Quem escreve o teste que falha é quem define o contrato.

## Vertical slicing (correto) vs Horizontal slicing (anti-padrão)

- ❌ Todos os testes → toda implementação (horizontal)
- ✅ Um teste → implementação → próximo teste (vertical)

## O teatro de coverage

Teste escrito DEPOIS do código = "espelho autorreferente". O agente confirma o que ele mesmo fez, inclusive bugs. Coverage de 92% pode ter mutation score de 4%.

## O paradoxo do METR

Devs em projetos bem testados são mais lentos com IA (METR). Isso é **bom**: significa que têm padrão alto e não aceitam output medíocre. São eles que não botam bug em produção.

## TDD pragmático na era IA

- Testar todo comportamento crítico ANTES de pedir implementação
- Buscar mutation score alto, não coverage alta
- Usar agente para gerar PBT a partir de invariantes que VOCÊ define
- Agente pode escrever testes de integração/e2e como complemento

## Ver também

- [[wiki/concepts/mutation-testing]]
- [[wiki/concepts/property-based-testing]]
- [[wiki/concepts/sensores-computacionais]]
