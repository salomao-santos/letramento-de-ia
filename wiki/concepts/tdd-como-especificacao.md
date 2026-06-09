---
title: "TDD como Especificação"
type: concept
tags: [tdd, testes, especificação, coding-com-ia]
created: 2026-06-08
updated: 2026-06-09
sources: ["[[wiki/sources/tdd-na-era-dos-agentes]]", "[[wiki/sources/engenharia-era-piloto-automatico]]", "[[wiki/sources/software-fundamentals-matter-more-than-ever]]", "[[wiki/sources/full-walkthrough-workflow-ai-coding]]"]
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

## TDD como limite de velocidade (Matt Pocock)

[[wiki/entities/matt-pocock|Matt Pocock]] reformula: "a taxa de feedback é seu limite de velocidade" (conceito de *outrunning your headlights* do Pragmatic Programmer). A IA por padrão gera muito código antes de validar. TDD força small steps obrigatórios.

No workshop prático, Matt demonstra TDD dentro do **Ralph loop** (implementação AFK):
- O agente escreve um teste que falha (RED), confirma a falha, implementa (GREEN)
- Isso é "absolutely essential" porque sem feedback loops o agente "codes blind"
- TDD torna mais difícil colar porque o código é instrumentado antes de existir
- Resultado empírico: codebase de workshop passou a ter 284 testes com qualidade razoável

> "If your code base doesn't have feedback loops, you're never ever ever going to get decent output out of AI."

Complemento: codebases com **deep modules** (interfaces simples, muita funcionalidade interna) são mais testáveis porque se testa na interface. Isso cria um ciclo virtuoso: deep modules → facilidade de teste → TDD funciona melhor → codebase melhora → IA produz melhor código.

## TDD como Harness (Zarathon)

Na visão expandida de [[wiki/entities/zarathon-viana]], TDD é literalmente um harness — um "cercado" que define os critérios aceitos:

> "São esses critérios que eu aceito que você me ajude a criar dentro desse cercadinho."

Implicações:
- Codebase facilmente testável = facilmente alterável = saudável
- Software de mais qualidade e previsibilidade como efeito colateral
- Em brownfield (95% da indústria), primeiro estruturar camada de QA antes de usar IA
- Mutation testing para identificar testes que ainda faltam

## Ver também

- [[wiki/concepts/mutation-testing]]
- [[wiki/concepts/property-based-testing]]
- [[wiki/concepts/sensores-computacionais]]
- [[wiki/concepts/sanity-checks]]
- [[wiki/concepts/ambient-affordances]] — deep modules como affordance que facilita TDD
- [[wiki/sources/software-fundamentals-matter-more-than-ever]]
