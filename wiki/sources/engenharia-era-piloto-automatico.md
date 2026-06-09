---
title: "Engenharia de Software na Era do Piloto Automático"
type: source
tags: [automação, aviação, formação, ddd, software-design, multimodelo, harness, tdd, avaliação, liderança]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[raw/clippings/Engenharia de software na era do piloto automático - Zarathon Viana]]"]
author: "Zarathon Viana"
published: 2026-06-05
format: "Podcast (Tech Leadership Rocks #247)"
---

# Engenharia de Software na Era do Piloto Automático

## Resumo

Episódio de podcast onde Zarathon Viana expande a analogia aviação-dev, discutindo DDD e software design como skills fundamentais, futuro multimodelo/SLM, TDD como harness, formação de novos engenheiros, avaliação de desempenho, sanity checks para codebases, e o papel do líder técnico na era da IA.

## Tese Central

> "Escrever código é uma coisa, escrever software é outra coisa. Software precisa de código, mas nem todo código é software."

## Conceitos-chave

### Skills que importam agora

O engenheiro que é "só coder" precisa subir um nível: entender o domínio do negócio e fazer design de software. Dois livros como base:
- **"Aprendendo Domain Driven Design"** (O'Reilly) — mapear o mundo real pro virtual
- **"A Philosophy of Software Design"** — pensar design de forma estruturada

Quem sabe mapear o mundo real e resolver com código não fica desempregado independente do paradigma.

### Greenfield vs Brownfield

- **Greenfield:** fazer coisa nova com IA é trivial. Se faz cagada no greenfield, precisa rever conceitos.
- **Brownfield (95% da indústria):** código legado que provavelmente não é "AI ready". Necessidade de uma **fase de setup** para preparar codebases existentes para IA.

### Futuro multimodelo e SLMs

Visão de 5-10 anos: multiagente, multimodelo. LLMs genéricos → SLMs (Specific/Small Language Models):
- Pequenos o suficiente para rodar na máquina local (~200MB)
- Cada empresa pode criar SLMs fine-tunados para seu domínio
- Exemplo: SLM fine-tunado em Qwen 2.5 para código Go

**Curto prazo (1-2 anos):** modelos híbridos — LLMs caros para raciocínio profundo + open models (Qwen, DeepSeek) para implementação. Custo deve subir ~10x quando subsídios acabarem.

**Workflow prático (Matos):** Opus para design/thinking + Qwen para implementação.

### TDD como regra e Harness

TDD agora é regra, não opção. Serve como "cercado" que define os critérios aceitos:
> "São esses critérios que eu aceito que você me ajude a criar dentro desse cercadinho."

Harness engineering não é só tooling — é também **comunicação**. Token efficiency: quem não se comunica bem gasta tokens e tempo no pingpong. Quanto mais direto e sem ambiguidade, melhor o output.

### Instrumentalização e sensores

Logs e traces como "breadcrumbs" para a IA resolver bugs. Custo caiu a quase zero:
> "Não tem mais porque não colocar log, não tem mais porque não colocar um trace. Antigamente a gente passava um dia fazendo só isso."

MCPs para observabilidade (Grafana, Datadog, New Relic) + ADRs como base de conhecimento para debugging assistido por IA.

### Formação de novos engenheiros

Analogia com contabilidade e aviação: primeiro aprende na munheca, depois usa ferramentas.
- **Problem based learning:** dar problema, resolver sem IA. Depois resolver com IA para ver a diferença.
- **Pair programming sênior-júnior:** buddies por período longo. Sênior ensina manual, depois ensina com IA. Repete 10-20x.
- IA catalisa o output: quem tem base acelera resultado bom; quem não tem acelera resultado ruim.
- Loop de repertório será mais rápido que antes, mas cuidado com burnout.

### Avaliação de desempenho na era IA

Volume de entrega vai nivelar todo mundo. O que diferencia:
- Envolvimento com negócio
- Soft skills: colaboração, curiosidade, suporte ao time
- Reação a incidentes
- Comunicação assertiva

> "Times menores de pessoas altamente colaborativas, curiosas, que se suportam e estão envolvidas com negócio."

### Caixa preta e Kaizen para agentes

Prática de "post-mortem de agentes" — rotina semanal que:
1. Pega todas as sessões da semana
2. Extrai lições aprendidas
3. Refatora o set de skills/regras do agente

Analogia: caixa preta da aviação → melhoria contínua do setor inteiro.

### Pré-mortem para qualidade intencional

Antes de subir feature: gerar cenários de pré-mortem → criar testes → deploy com canário (1%) → rodar cenários de pré-mortem no canário → qualidade intencional a cada deploy.

### Sanity checks para codebases

"Cheque de sanidade" automatizado no CI: antes de ir pro ar, verifica se mudança mantém código sadio. Pode usar multimodelos/multiagentes para validação cruzada. Evolução do Sonar para o codebase inteiro.

**Feed forward vs feedback (Fowler):** Feed forward é importante, mas feedback é mais crucial — garantir compliance com decisões tomadas no design.

### O líder do futuro

- Mais técnico que antes (tão técnico quanto staff engineer)
- Não cobrado por código, mas por **conhecimento técnico** do que vai pro ar
- Usa IA para inspecionar codebase e criar arcabouço de comunicação com negócio
- Negocia factibilidade em 15 minutos (antes levava 1 dia)
- Protege time: equilibra empolgados (risco de burnout) e reticentes (precisam ganhar confiança)

### Processo seletivo

- Não faz mais sentido: desafio take-home, reordenar árvore, algoritmo puro
- Faz sentido: abrir codebase com problemas e ver como candidato investiga
- Avaliar: criatividade, base conceitual, comunicação clara, entendimento de tradeoffs
- Token efficiency como habilidade: expressar intenção com clareza e pragmatismo

## Livros Recomendados

| Livro | Para quem |
|-------|-----------|
| Aprendendo Domain Driven Design (O'Reilly) | Todos — mapear mundo real → virtual |
| A Philosophy of Software Design | Todos — pensar design de forma estruturada |
| Design of Design (Fred Brooks) | Veteranos — metamodelo de design |

## Frases-chave

- "A gente nunca fez o software como deveria ter sido feito. Agora não tem mais essa desculpa."
- "O código ficou barato."
- "Quem não tem base vai acelerar um output ruim."
- "Harness não é só tooling, harness também é comunicação."
- "O futuro é dos criativos."
- "Esse negócio não tem mais rollback."

## Conceitos Relacionados

- [[wiki/concepts/horas-de-voo-para-devs]]
- [[wiki/concepts/harness-engineering]]
- [[wiki/concepts/tdd-como-especificacao]]
- [[wiki/concepts/tres-camadas-coding-ia]]
- [[wiki/concepts/automation-complacency]]
- [[wiki/concepts/sensores-computacionais]]
- [[wiki/concepts/sanity-checks]]
- [[wiki/concepts/multimodelo-slm]]
- [[wiki/concepts/formacao-novos-engenheiros]]

## Ver também

- [[wiki/sources/devs-sao-os-novos-pilotos]] — artigo original da analogia aviação-dev
- [[wiki/sources/as-3-camadas-do-coding-com-ia]] — framework de 3 camadas
- [[wiki/entities/zarathon-viana]]
