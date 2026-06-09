---
title: "Clean Architecture está te CUSTANDO CARO na era da IA"
type: source
tags: [arquitetura, clean-architecture, yagni, custo-de-contexto, ddd-estrategico]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[raw/clippings/Clean Architecture está te CUSTANDO CARO na era da IA]]"]
---

# Clean Architecture está te CUSTANDO CARO na era da IA

## Metadados

- **Autor:** [[wiki/entities/waldemar-neto]]
- **Canal:** YouTube (Tech Leads Clube)
- **Data:** 2025-06-26
- **Duração:** ~16 min
- **URL:** https://www.youtube.com/watch?v=qLEg0PLWj2k

## Resumo

Vídeo que questiona a implementação ritualística de Clean Architecture na era dos agentes de IA. Argumento central: os princípios (lógica isolada, testabilidade, encapsulamento) continuam válidos, mas a cerimônia tática (interfaces por repositório, use cases por CRUD, múltiplas camadas de DTOs/mappers) tem custo mensurável em tokens, acurácia da IA e velocidade de feature.

## Tese principal

> "Quanto da arquitetura que a gente defendeu por décadas era sobre código e quanto era sobre os nossos próprios limites?"

A hipótese: muitas abstrações que adotamos não eram pelo benefício do código, mas para compensar a dificuldade humana de navegar codebases grandes. E agora, com IA, essas abstrações não só não ajudam como aumentam o custo (tokens, indireções, confusão de contexto).

## Argumentos-chave

### 1. A indústria já simplificava antes da IA

Go, Rust, Kotlin e Java moderno são menos verbosos. Go não tem classes, herança ou anotações — mas Kubernetes, Docker e Cloudflare implementam os princípios fundamentais de Clean Architecture (isolamento, DI, testabilidade) sem a cerimônia.

> "O princípio sempre foi separável da prática."

### 2. Custo mensurável por token

- Cada arquivo a mais = token a mais no contexto do agente
- Cada indireção = pulo a mais para IA entender o fluxo
- Cada abstração sem propósito real = ruído competindo com lógica que importa

### 3. Paper "Navigation Paradox" (2026)

Mediu o custo das abstrações para agentes:
- DI/DIP criam conexões que existem no runtime mas não no código fonte — IA não descobre
- Claude Code acerta ~76% dos arquivos necessários em tarefas com dependência escondida
- Pastas por camada (domain/application/infrastructure/presentation) forçam 7-13 arquivos por feature
- Mesmo com ferramenta de navegação, o agente ignora 58% das vezes ("glob e read já me dão 80%")

### 4. Abstraction Bloat (Addy Osmani, Google)

Agente sem supervisão escreve 1000 linhas onde 100 bastariam. Motivo: dados de treinamento super-representam blogs sobre padrões complexos. Ninguém publica "fiz um CRUD com 3 arquivos e funciona há 5 anos".

### 5. Abstraction Illusion (Super Productivity)

> "A IA torna padrões sofisticados acessíveis sem torná-los apropriados."

Antes, implementar Event Sourcing exigia livro + estudo + construção incremental — esse processo filtrava. Hoje, 2 prompts e está lá para um sistema que nunca precisará.

### 6. YAGNI escalado pela IA

A IA não criou o problema de abstração preventiva — ela escalou. Agora tu gera abstração em minutos, não em dias. E o custo só aparece depois.

### 7. DDD Estratégico ficou MAIS importante

O que ficou crítico:
- **Bounded Context** = escopo menor de arquivos = menos tokens = melhor acurácia
- **Linguagem ubíqua** = prompts com termos do domínio = código mais fiel ao negócio
- **Separação por domínio** = aponta agente para um contexto só

O que é questionável:
- Interface por repositório (só se múltiplas implementações reais)
- Use case por CRUD (problema real que resolve?)
- Mappers entre 3 camadas de DTO (3 camadas para mesma info?)

### 8. Encapsulamento ≠ Inversão de dependência

- **Encapsulamento:** esconder o detalhe. UserRepository.find() — ninguém sabe do Prisma. Se trocar, só 1 arquivo muda. Sem interface, sem cerimônia.
- **Inversão de dependência (DIP):** ambos dependem de abstração (interface no meio). Inverte a direção da dependência, mas cria indireção + boilerplate + carga cognitiva.

### 9. Regra prática: "Estratégico primeiro, flat depois, abstrai por dor"

1. **Módulos por domínio** (billing, orders, identity) — cada pasta independente. DDD estratégico barato.
2. **Flat dentro do módulo** — entrada/saída + lógica + persistência. 3 responsabilidades claras, sem interface/ports/adapters/mappers.
3. **Abstrai só quando a dor justificar:**
   - Trocou essa dependência nos últimos 2 anos? Se não, não abstrai.
   - Tem 2º uso real? Se sim, extrai (nunca antecipado).
   - Medo de contrato externo poluir domínio? Interface numa ACL.

### 10. Contra-argumento honesto

"Se IA gera 10x mais rápido, ausência de estrutura vira caos 10x mais rápido."

Resposta: limites são importantes, mas podem vir de lugares baratos:
- Bounded contexts + pastas por domínio
- Tipos fortes nos contratos entre módulos
- Testes de comportamento (não implementação)
- Lint rules que impedem import entre domínios

## Conceitos referenciados

- [[wiki/concepts/ambient-affordances]] — organização por domínio como affordance
- [[wiki/concepts/harness-engineering]] — lint rules e testes como sensors baratos
- [[wiki/concepts/sensores-computacionais]] — lint que impede imports cruzados
- [[wiki/concepts/tres-camadas-coding-ia]] — camada 3 (arquitetura) como alto controle

## Dados e referências citados

- Paper "Navigation Paradox" (2026) — custo de abstrações para agentes
- Addy Osmani (Google) — "abstraction bloat"
- Super Productivity (artigo) — "abstraction illusion"
- Kent Beck — YAGNI (1999, Extreme Programming Explained)
- Eric Evans — DDD (Bounded Context, Ubiquitous Language)
- Uncle Bob (Robert C. Martin) — Clean Architecture, SOLID, DIP

## Relação com outras fontes

- Complementa [[wiki/sources/arquitetura-na-era-dos-agentes]] (mesma tese, aqui com dados quantitativos)
- Reforça [[wiki/sources/software-fundamentals-matter-more-than-ever]] (deep modules vs shallow = flat vs ritualístico)
- Converge com [[wiki/sources/full-walkthrough-workflow-ai-coding]] (vertical slices, token-efficiency)
- Tensiona com [[wiki/sources/harness-engineering-fowler]] (DIP como ferramenta de controle vs custo de contexto)
