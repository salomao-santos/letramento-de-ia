---
title: "Custo de Abstrações na Era da IA"
type: concept
tags: [arquitetura, clean-architecture, yagni, tokens, custo-de-contexto, ddd-estrategico]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[wiki/sources/clean-architecture-custando-caro-era-ia]]", "[[wiki/sources/arquitetura-na-era-dos-agentes]]", "[[wiki/sources/software-fundamentals-matter-more-than-ever]]"]
---

# Custo de Abstrações na Era da IA

## Definição

Na era dos agentes de coding, cada abstração arquitetural tem um custo mensurável em tokens, acurácia e velocidade de entrega. Abstrações que antes serviam para compensar limitações humanas de navegação agora pesam duplamente: poluem o contexto da IA e ainda não ajudam o humano tanto quanto prometiam.

## O princípio vs. a cerimônia

O princípio (lógica isolada, encapsulamento, testabilidade) continua válido. O que é questionável é a implementação ritualística:

| Ritualístico (custo alto) | Essencial (custo baixo) |
|---------------------------|------------------------|
| Interface para cada repositório | Encapsulamento sem interface |
| Use case para cada CRUD | Separação lógica/HTTP/SQL |
| Mappers entre 3 camadas de DTO | Tipo forte no contrato |
| Pastas por camada (domain/app/infra/presentation) | Pastas por domínio (billing/orders/identity) |

## Custo mensurável

- **Cada arquivo a mais** = token a mais no contexto do agente
- **Cada indireção** = pulo a mais para IA entender o fluxo
- **Cada abstração sem propósito real** = ruído competindo com lógica que importa
- **DI/DIP** cria conexões invisíveis no código fonte (existem só em runtime)

## Paper "Navigation Paradox" (2026)

Mediu o impacto concreto:
- Claude Code acerta ~76% dos arquivos em tarefas com dependência escondida (perde 1 em 4)
- Pastas por camada forçam 7-13 arquivos por feature (vertical slices: 1)
- Mesmo com MCP de navegação, agente ignora 58% das vezes (heurística: "glob+read já dão 80%")

## Abstraction Bloat e Abstraction Illusion

- **Abstraction Bloat** (Addy Osmani/Google): agente sem supervisão escreve 1000 linhas onde 100 bastariam. Dados de treinamento super-representam padrões complexos.
- **Abstraction Illusion** (Super Productivity): a IA torna padrões sofisticados acessíveis sem torná-los apropriados. O processo de aprendizado antes filtrava — agora 2 prompts geram Event Sourcing para um sistema que nunca precisará.

## YAGNI escalado

[[wiki/entities/kent-beck]] cunhou YAGNI em 1999. Na era da IA, o problema escalou: abstração preventiva que levava dias agora é gerada em minutos, mas o custo de manutenção permanece.

> "A maioria dos 'e se um dia' nunca acontece. E quando acontece, a realidade é tão diferente do que tu imaginou que a abstração que era para ajudar atrapalha."

## DDD Estratégico como otimização de contexto

O que ficou **mais** importante:
- **Bounded Context** = escopo menor = menos tokens = IA acerta mais
- **Linguagem ubíqua** = prompts com termos do domínio = código mais fiel
- **Módulos por domínio** = aponta agente para 1 contexto só

## Encapsulamento ≠ Inversão de dependência

Confusão frequente:
- **Encapsulamento:** esconder detalhe. `UserRepository.find()` — ninguém sabe do Prisma. Se trocar, 1 arquivo muda. Sem interface.
- **Inversão de dependência (DIP):** ambos dependem de abstração (interface no meio). Inverte direção da dependência, mas cria indireção + boilerplate + carga cognitiva para humano e IA.

## Regra prática

> "Estratégico primeiro, flat depois, abstrai por dor."

1. **Módulos por domínio** — DDD estratégico barato (é só pasta)
2. **Flat dentro do módulo** — 3 responsabilidades (entrada/lógica/persistência), sem cerimônia
3. **Abstrai só quando dor justificar:**
   - Trocou dependência nos últimos 2 anos? Não → não abstrai
   - 2º uso real? Sim → extrai (nunca antecipado)
   - Contrato externo poluindo domínio? → Interface numa ACL

## Contra-argumento

"Se IA gera 10x mais rápido, ausência de estrutura vira caos 10x mais rápido."

Resposta: limites baratos bastam — bounded contexts, tipos fortes, testes de comportamento, lint rules bloqueando imports cruzados. Estrutura sem custo de 18 arquivos por feature.

## Ver também

- [[wiki/concepts/ambient-affordances]] — deep modules e organização por domínio
- [[wiki/concepts/tres-camadas-coding-ia]] — arquitetura como camada de alto controle
- [[wiki/concepts/harness-engineering]] — sensores como limites baratos
- [[wiki/concepts/sensores-computacionais]] — lint que impede imports cruzados
- [[wiki/sources/clean-architecture-custando-caro-era-ia]] — fonte principal
- [[wiki/sources/arquitetura-na-era-dos-agentes]] — mesma tese, foco em cercas

## Referências

- [[wiki/sources/clean-architecture-custando-caro-era-ia]]
- [[wiki/sources/arquitetura-na-era-dos-agentes]]
- [[wiki/sources/software-fundamentals-matter-more-than-ever]]
