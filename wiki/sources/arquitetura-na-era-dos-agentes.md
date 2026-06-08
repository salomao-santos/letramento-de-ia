---
title: "Arquitetura de software na era dos agentes: a cerca que o LLM não pula"
type: source
tags: [arquitetura, clean-architecture, ddd, bounded-context, sensores-computacionais]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[raw/clippings/Arquitetura de software na era dos agentes a cerca que o LLM não pula]]"]
author: "Zarathon Viana"
published: 2026-05-06
---

# Arquitetura de software na era dos agentes

## Resumo

Segundo artigo da série. Defende que arquitetura explícita (Clean Architecture, Hexagonal, DDD) deixou de ser "overkill" e virou necessidade prática na era dos agentes de coding. O LLM resolve problemas locais brilhantemente, mas não pensa globalmente — cria dependências circulares, embaralha camadas e pega atalhos. Cercas arquiteturais são o antídoto.

## Tese Central

> "A velocidade do LLM sem cerca arquitetural é velocidade pra chegar no lugar errado mais rápido."

## Conceitos-chave

### LLM embaralha camadas
O LLM otimiza localmente. Importa helpers de outros módulos, puxa tipos da infra pro domínio, referencia config direto no use case. Cada atalho faz sentido isoladamente; acumulados, geram big ball of mud.

### Clean Architecture / Hexagonal como cercas
Camadas explícitas + direção de dependência definida = o agente não tem pra onde ir. O linter barra importações proibidas.

### DDD aplicado a agentes
- **Bounded Contexts** como cercas semânticas — o agente sabe onde está
- **Linguagem Ubíqua** como contexto pro LLM — o agente usa os termos certos
- **Aggregates** como unidades de mudança — escopo de alteração contido

### Sensores computacionais para drift arquitetural
- Java: [[wiki/entities/archunit]]
- JavaScript/TypeScript: [[wiki/entities/dependency-cruiser]]
- Qualquer stack: Danger

### Ambient affordances
Propriedades estruturais do ambiente que o tornam legível e navegável por agentes: estrutura de pastas, convenções de nomenclatura, service templates.

## Caso prático: Time A vs Time B
- **Time A** (arquitetura explícita): monorepo com bounded contexts, ArchUnit no CI, glossário de domínio. Agente entregou respeitando fronteiras. Deploy sem incidente.
- **Time B** (arquitetura implícita): pastas por tipo, sem teste de dependência. Agente criou acoplamento. Quebrou 2 semanas depois.

## Dados-chave
- DORA 2025: times com arquitetura frouxamente acoplada + feedback loops rápidos = 20-30% ganho de produtividade e 50% mais "Happy Time"
- Adidas: caso citado no DORA com ganhos mensuráveis

## Checklist do artigo
1. Materialize fronteiras no código
2. Instale sensores de arquitetura no CI
3. Documente a linguagem ubíqua
4. Defina bounded contexts explícitos
5. Crie service templates
6. Prefira organização por domínio, não por tipo
7. Rode ArchUnit/dependency-cruiser como teste, não lint
8. Faça a arquitetura chata

## Conceitos Relacionados
- [[wiki/concepts/tres-camadas-coding-ia]]
- [[wiki/concepts/sensores-computacionais]]
- [[wiki/concepts/ambient-affordances]]
- [[wiki/concepts/harness-engineering]]

## Referências
- Fowler & Böckeler (2026): https://martinfowler.com/articles/harness-engineering.html
- Russ Miles (2025): https://engineeringagents.substack.com/p/domain-driven-agent-design
- ArchUnit: https://www.archunit.org/
- dependency-cruiser: https://github.com/sverweij/dependency-cruiser
