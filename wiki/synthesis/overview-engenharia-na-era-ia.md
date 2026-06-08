---
title: "Síntese: Engenharia de Software na Era dos Agentes de IA"
type: synthesis
tags: [síntese, overview, engenharia-de-software, agentes-ia, harness-engineering]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[wiki/sources/as-3-camadas-do-coding-com-ia]]", "[[wiki/sources/arquitetura-na-era-dos-agentes]]", "[[wiki/sources/devs-sao-os-novos-pilotos]]", "[[wiki/sources/tdd-na-era-dos-agentes]]", "[[wiki/sources/code-review-na-era-dos-agentes]]", "[[wiki/sources/harness-engineering-fowler]]", "[[wiki/sources/maintainability-sensors]]", "[[wiki/sources/spec-driven-development]]", "[[wiki/sources/engenharia-era-piloto-automatico]]"]
---

# Engenharia de Software na Era dos Agentes de IA

Síntese de 9 fontes processadas nesta wiki, conectando os argumentos de [[wiki/entities/zarathon-viana]] (série "As 3 camadas do coding com IA") com o trabalho de [[wiki/entities/birgitta-bockeler]] e [[wiki/entities/martin-fowler]] (Harness Engineering, Maintainability Sensors, Spec-Driven Development).

---

## A Tese Central

A IA generativa aplicada ao coding é um **amplificador**, não um corretor. Amplifica o que já existe: disciplina vira produtividade; falta de disciplina vira dívida técnica em velocidade industrial.

> "A IA não conserta um time; ela amplifica o que já está lá." — DORA 2025

O engenheiro que se destaca neste cenário não é o que prompta melhor, mas o que **constrói cercas determinísticas** ao redor de um modelo probabilístico.

---

## O Framework: 3 Camadas de Controle

([[wiki/concepts/tres-camadas-coding-ia]])

```
Camada 1 — Modelo       → controle baixo  (escolhe)
Camada 2 — Ferramenta   → controle médio  (configura, estende)
Camada 3 — Engenharia   → controle alto   (escreve, define, audita)
```

**Insight:** A maioria da comunidade investe energia na camada 2 (MCPs, prompts, context engineering). Mas a camada 3 oferece mais alavanca por hora investida. Camada 3 é investment capital; as outras são running cost.

---

## Os Três Pilares da Camada 3

### 1. Arquitetura → define POR ONDE o agente pode ir

([[wiki/sources/arquitetura-na-era-dos-agentes]])

O LLM otimiza localmente. Sem cercas, cria dependências circulares, embaralha camadas, pega atalhos. Cada atalho faz sentido isoladamente; acumulados, geram big ball of mud.

**Antídoto:** Clean Architecture, Hexagonal, DDD com bounded contexts explícitos + sensores computacionais (ArchUnit, dependency-cruiser) que **quebram o build** em violações.

### 2. Testes → define O QUE o agente deve produzir

([[wiki/sources/tdd-na-era-dos-agentes]])

Na era dos agentes, teste não é verificação — é **especificação**. O custo de gerar código caiu pra quase zero; o que ficou caro é especificar intenção. Teste é a forma mais determinística de fazer isso.

**Ciclo:** Humano escreve teste (RED) → Agente implementa (GREEN) → Colaboração refatora (REFACTOR)

**Regra de ouro:** nunca delegar o RED pro agente.

### 3. Code Review → define SE pode passar

([[wiki/sources/code-review-na-era-dos-agentes]])

O último portão humano antes de produção. O LLM gera código "quase certo" — plausível, bem escrito, e errado de formas sutis. O reviewer precisa caçar o erro convincente, não o erro óbvio (que a máquina já pega).

**Fluxo ideal:** CI (gates duros) → IA review (sensor) → Autor corrige → Humano revisa (juiz)

---

## O Modelo de Harness Engineering

([[wiki/sources/harness-engineering-fowler]], [[wiki/concepts/harness-engineering]])

Fórmula canônica: **Agent = Model + Harness**

### Taxonomia

|  | Feedforward (Guides) | Feedback (Sensors) |
|--|---------------------|-------------------|
| **Computational** | Scripts, codemods, LSPs | Testes, linters, type checkers, ArchUnit |
| **Inferential** | AGENTS.md, Skills, specs | Review agents, "LLM as judge" |

### Categorias de regulação
1. **Maintainability** — qualidade interna (mais fácil de implementar hoje)
2. **Architecture Fitness** — fitness functions
3. **Behaviour** — o "elefante na sala" (ainda muito a resolver)

### O Steering Loop
Sempre que um problema ocorre múltiplas vezes, melhorar os controles para torná-lo menos provável no futuro. O humano itera no harness; o agente trabalha dentro dele.

---

## Sensores na Prática

([[wiki/sources/maintainability-sensors]], [[wiki/concepts/sensores-computacionais]])

Böckeler experimentou em projeto real (TypeScript/NextJS) e documentou:

| Quando | Sensores |
|--------|----------|
| Durante coding | Type checker, ESLint, Semgrep, dependency-cruiser, testes, mutation testing incremental, GitLeaks |
| Pipeline (CI) | Todos os acima repetidos em ambiente limpo |
| Periodicamente | Security review (IA), data handling review (IA), dependency freshness, modularity review |

### Aprendizados-chave
- Custom lint messages = "positive prompt injection" (fazem diferença real no comportamento do agente)
- Sensores computacionais: excelentes no nível arquivo/função
- Cross-file concerns: precisam de sensor inferencial (IA) para interpretação semântica
- **Mutation testing é crucial** quando testagem é delegada à IA

---

## A Analogia com a Aviação

([[wiki/sources/devs-sao-os-novos-pilotos]], [[wiki/concepts/automation-complacency]])

O voo Air France 447 (2009) como metáfora: quando o autopilot falha, só quem tem "horas de voo manual" assume. Três fenômenos documentados em aviação que se replicam em dev:

1. **Perda de habilidades manuais** — devs que nunca debugaram sem IA
2. **Perda de consciência situacional** — não entender o que o sistema faz
3. **Automation complacency** — confiar demais, verificar de menos

**Dado perturbador:** Estudo METR mostrou devs 19% mais lentos com IA, mas percebendo 20% mais rápidos. Diferença de percepção de ~40 pontos percentuais.

**Antídoto:** acumular "horas de voo" — projetos próprios, open source, freelance, build in public ([[wiki/concepts/horas-de-voo-para-devs]])

---

## Multimodelo e Sustentabilidade Econômica

([[wiki/concepts/multimodelo-slm]], [[wiki/sources/engenharia-era-piloto-automatico]])

Modelos atuais são subsidiados (custos devem subir ~10x). A resposta é diversificação:

| Fase | Estratégia |
|------|-----------|
| Agora | LLMs subsidiados |
| 1-2 anos | Híbrido: LLM caro (raciocínio) + open models (implementação) |
| 5-10 anos | SLMs fine-tunados por domínio, rodando localmente (~200MB) |

**Workflow prático:** Opus para design/thinking + Qwen/DeepSeek para implementação. Resultados comparáveis a 1/5 do custo.

---

## Formação de Novos Engenheiros

([[wiki/concepts/formacao-novos-engenheiros]], [[wiki/sources/engenharia-era-piloto-automatico]])

O caminho tradicional (tarefas simples → aprender com seniors) está sendo corroído pela IA. Propostas:

1. **Problem based learning:** resolver primeiro sem IA, depois com IA
2. **Pair programming sênior-júnior:** buddies por período longo, repetir 10-20x
3. **Horas de voo manual obrigatórias:** deploy, monitoramento, debug na mão

> "A IA catalisa o output. Quem tem base acelera resultado bom; quem não tem acelera resultado ruim."

---

## Sanity Checks e Qualidade Intencional

([[wiki/concepts/sanity-checks]], [[wiki/sources/engenharia-era-piloto-automatico]])

Evolução do Sonar: verificações automatizadas no CI que validam se mudanças mantêm o codebase sadio.

- **Determinístico:** linters, type checkers, fitness functions
- **Probabilístico:** multimodelos validando em consenso
- **Pré-mortem:** gerar cenários de falha → criar testes → canário → validação proativa

> "A gente nunca fez o software como deveria ter sido feito. Agora não tem mais essa desculpa."

---

## Spec-Driven Development: Promessa e Limites

([[wiki/sources/spec-driven-development]], [[wiki/concepts/spec-driven-development]])

Abordagem que propõe spec antes de código. Três níveis: spec-first, spec-anchored, spec-as-source.

### Valor real
O princípio de pensar e estruturar antes de pedir ao agente é valioso.

### Limites (Böckeler)
- Workflows one-size-fits-all não funcionam para todas as escalas
- Muitos markdowns para revisar pode ser **pior** que revisar código
- Agente frequentemente ignora partes da spec (context window maior ≠ absorção total)
- Risco de **Verschlimmbesserung** — piorar na tentativa de melhorar

### Relação com TDD
TDD é uma alternativa/complemento determinístico: o teste como spec executável. Não sofre de não-determinismo como specs em linguagem natural.

---

## O Gradiente Determinístico → Probabilístico

Uma ideia transversal a todas as fontes:

```
Determinístico (confiável)                    Probabilístico (não-confiável)
────────────────────────────────────────────────────────────────────────────
Testes    Linters    ArchUnit    Type check  │  LLM gera    LLM revisa    LLM spec
                                             │
←── Sensores computacionais ──────────────── │ ── Sensores inferenciais ──→
```

A engenharia de software clássica vive no lado esquerdo. O LLM vive no lado direito. O harness é a ponte que faz os dois trabalharem juntos de forma produtiva.

Pela primeira vez na história, o salto de abstração não é determinístico→determinístico (Assembly→C→Java→Frameworks), mas **determinístico→probabilístico**. Isso muda fundamentalmente a natureza do trabalho.

---

## Dados que Sustentam a Tese

| Fonte | Dado |
|-------|------|
| METR 2025 | Devs seniores 19% mais lentos com IA (percebem 20% mais rápidos) |
| DORA 2025 | 90% usam IA; instabilidade de entrega continua subindo |
| DORA 2025 | Times com arquitetura frouxamente acoplada + feedback loops = +20-30% produtividade |
| GitClear | Code churn quase dobrou no período de adoção de IA (211M linhas) |
| Stack Overflow 2025 | 66% frustrados com soluções "quase certas"; 45% gastam mais tempo debugando IA |
| Stanford/ADP 2025 | Emprego de devs 22-25 anos caiu ~20% desde pico de 2022 |
| Código Fonte TV 2025 | 95,5% dos devs brasileiros usam IA |
| Anthropic 2024 | Margem bruta negativa de 94% (subsídio insustentável) |
| Zarathon 2026 | Brownfield = ~95% da indústria; maioria não está "AI ready" |
| Zarathon 2026 | Custo de modelos deve subir ~10x quando subsídios acabarem |
| Zarathon 2026 | SLM fine-tunado de 200MB já entrega resultados comparáveis para tarefas específicas |

---

## O Checklist do Engenheiro (Consolidado)

Unificando as recomendações práticas de todas as 9 fontes:

1. **Materialize fronteiras no código** — bounded contexts, pastas por domínio
2. **Instale sensores de arquitetura no CI** — ArchUnit, dependency-cruiser, Danger
3. **Documente a linguagem ubíqua** — glossário no root do repo
4. **Escreva teste ANTES do código** — TDD como especificação, vertical slicing
5. **Use mutation testing** — detector de mentira para suítes frágeis
6. **PRs pequenos (200-400 linhas)** — um propósito por PR
7. **IA review como sensor, humano como juiz** — fluxo em sequência
8. **Conventional commits** — histórico legível para volume industrial
9. **Rode tudo como teste (quebra build), não como lint (só avisa)**
10. **Mantenha "horas de voo manual"** — não delegue tudo ao agente
11. **Instrumentalize tudo com log/trace** — breadcrumbs para debug assistido (custo quase zero)
12. **Sanity checks no CI** — cheque de sanidade antes de ir pro ar
13. **ADRs como base de conhecimento** — cada decisão de design gera ADR consultável
14. **Rotina de "caixa preta" semanal** — extrair lições das sessões de agente e melhorar regras
15. **Diversifique modelos** — raciocínio em LLM caro, implementação em model open/barato

---

## Contradições e Tensões

> [!warning] Tensão: Velocidade vs Qualidade
> O mercado pressiona adoção rápida de IA (CEOs, boards, investidores). Mas os dados mostram que adoção sem disciplina **aumenta** instabilidade. A pressão vem de cima; quem paga o preço é quem está na cabine.

> [!warning] Tensão: Spec-Driven vs TDD
> SDD propõe spec em linguagem natural como fonte da verdade. TDD propõe teste como spec executável. Böckeler questiona se SDD elaborado não é Verschlimmbesserung. As abordagens podem ser complementares (spec para alto nível, teste para contrato determinístico).

> [!warning] Tensão: Sensores computacionais vs inferenciais
> Computacionais são confiáveis mas limitados a estrutura. Inferenciais capturam semântica mas são não-determinísticos. A solução não é um ou outro, mas camadas: computacional como base + inferencial como complemento.

---

## Lacunas Identificadas

> [!question] Behaviour Harness
> Como guiar e verificar se a aplicação se comporta corretamente do ponto de vista funcional? Böckeler chama de "o elefante na sala". Nenhuma solução robusta ainda.

> [!question] Formação de novos devs
> Se a IA elimina as tarefas simples que formavam juniors, quem será senior daqui a 5 anos? O caminho tradicional de formação está sendo corroído. Zarathon propõe: problem based learning + pair sênior-júnior + horas de voo manual. O loop de repertório será mais rápido, mas a base ainda precisa de tempo ([[wiki/concepts/formacao-novos-engenheiros]]).

> [!question] Sustentabilidade econômica dos modelos
> OpenAI e Anthropic operam com prejuízo bilionário. Quando o subsídio acabar, preços podem subir ~10x. Resposta proposta: migrar para multimodelo/SLM, com modelos open para implementação e LLMs caros apenas para raciocínio profundo ([[wiki/concepts/multimodelo-slm]]).

---

## Ver também

- [[wiki/concepts/tres-camadas-coding-ia]] — o framework organizador
- [[wiki/concepts/harness-engineering]] — o modelo mental de controle
- [[wiki/concepts/sensores-computacionais]] — a camada determinística
- [[wiki/concepts/tdd-como-especificacao]] — teste como contrato
- [[wiki/concepts/code-review-como-portao]] — o portão humano
- [[wiki/concepts/automation-complacency]] — o risco psicológico
- [[wiki/concepts/spec-driven-development]] — spec como guia (com limites)
- [[wiki/concepts/sanity-checks]] — cheque de sanidade antes de produção
- [[wiki/concepts/multimodelo-slm]] — futuro multimodelo e SLMs
- [[wiki/concepts/formacao-novos-engenheiros]] — formação na era IA
