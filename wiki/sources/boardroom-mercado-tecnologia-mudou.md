---
title: "Boardroom 2606-01: O Mercado de Tecnologia Mudou"
type: source
tags: [mercado, adoção-ia, formação, spec-driven, tdd, code-review, multimodelo, brasil]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[raw/clippings/Boardroom 2606-01 - O Mercado de Tecnologia Mudou]]"]
---

# Boardroom 2606-01: O Mercado de Tecnologia Mudou

## Metadados

- **Participantes:** Salomão Santos (Accenture/consultoria), [[wiki/entities/zarathon-viana|Zarathon Viana]] (Quinto Andar)
- **Canal:** Prodops
- **Tipo:** Podcast/conversa (coluna mensal)
- **Data:** 2026-06-26
- **URL:** https://www.youtube.com/watch?v=nznwgwY3P2g
- **Duração:** ~50 min

## Formato

Dois lados do balcão: Salomão (consultoria, grandes empresas listadas em bolsa) e Zarathon (mercado/produto, Quinto Andar). Visão Brasil-first com olhar para EUA.

## Tese central

O mercado mudou, mas o 10x prometido ainda não vingou. O que está se consolidando: checkpoints determinísticos, code review como fase central, e DDD + Software Design + System Thinking como pilares para o futuro.

## Estado atual do mercado (metade de 2026)

### A promessa do 10x
- **Ainda não vingou**, mas está se aproximando
- Modelos melhorando "numa curva absurda" de fevereiro/2026 em diante
- Onboarding de novos devs: **quase 10x mais rápido** (conversar com código legado em 1-1.5 semanas vs meses)
- Ler código legado: o **primeiro grande ganho real** da IA na indústria
- Produtividade de escrita: "insana" com IAG como personal writer
- Mínimo 2x comparando consigo mesmo, usando apenas ferramentas mainstream

### Adoção corporativa
- Foi **uma das adoções historicamente mais rápidas** de todas as ondas
- Em menos de 1 ano, toda empresa já aprovou alguma ferramenta
- Dependência real de tokens: acabar tokens é "desesperador"
- Custo: vai ficar mais caro (modelos melhores, janelas maiores)

### Modelos locais vs SaaS
- Modelo de blend: SaaS para uso pesado + modelos 14B locais para ações específicas
- Local produz ~1.5x no mínimo

## Três disclaimers (Salomão)

1. **Não é bolha.** É nova era (industrial → serviços → internet → IA → robótica)
2. **Spec-driven vai vingar** mas ainda não está pronto. 20+ frameworks competindo, vai sobrar 2-3
3. **Já sou "sem X"** na consultoria com ferramentas internas. Não é realidade do mercado

## Três pilares para o futuro (Zarathon)

### 1. DDD (Domain-Driven Design)
- Mapear mundo real → mundo digital
- Linguagem ubíqua = ponteiro de inferência calibrado para o modelo
- "Se você já diz o que é, economizou várias partes racionais do cálculo"

### 2. Software Design
- Desacoplamento, padrões, Design of Design (Brooks)
- Modelos foram treinados em padrões estabelecidos — usar do jeito certo agora importa mais
- "O código é um bicho mole, você pode fazer o que quiser — agora precisa fazer do jeito certo"

### 3. System Thinking
- Como sistemas interagem entre si
- Habilidade pouco explorada na academia, ganha-se com prática
- DDD + Software Design + System Thinking = fazer qualquer sistema

## Workflow com checkpoints (Zarathon)

```
Requisitos → [CP1: Ambiguidade] → Design → [CP2: TDD] → Código → [CP3: LLM EVAL] → Code Review humano
```

### Checkpoint 1: Qualidade do requisito
- IA identifica ambiguidade no que está sendo pedido
- Escrever de forma diretiva, sem deixar a IA inferir
- Português é ambíguo; inglês é "token efficient"
- Livros clássicos de análise de requisitos (Craig Larman, 2006) voltam com força

### Checkpoint 2: TDD
- "Kent Beck vai morrer de felicidade" — TDD agora é realidade, não opção
- Critérios de aceite → testes → IA implementa para fazer passar
- Software fica com qualidade melhor "por efeito colateral"

### Checkpoint 3: LLM como avaliador
- Modelo diferente julga código + testes + resultados de checkpoints
- Multimodelo obrigatório (não pode ser o mesmo modelo julgando a si mesmo)
- "Ecos" do modelo: concordar consigo mesmo gera loop confirmatório

### Code Review humano (fase final)
- "Talvez a fase mais importante dentro do processo"
- Foco: regras de negócio do domínio, não performance do código
- Design evolutivo? Desacoplado? Fácil de testar? Autocontido?

## Viés da eloquência

> "LLM sabe estatisticamente qual o próximo token. Quando você constrói frases bem construídas — a eloquência — você vai ficar viciado nela."

Para código funciona igual: parece certo, é articulado, gera confiança. Na terceira ou quarta interação, o humano para de criticar. É o [[wiki/concepts/automation-complacency|viés da automação]] por outro ângulo.

## Código ≠ Engenharia

> "Existe muito código sem engenharia. Engenheiros vão ficar mais caros."

- Marketing, Design, PM — todos produzem código agora
- Mas nenhum produz engenharia (escalabilidade, resiliência, evolução)
- Consultorias vão se posicionar em "transformar POC em produto"
- O mercado será: "me dá aqui o que o Lovable fez e eu faço bumpar"

## Build to Learn vs Build to Earn

| Build to Learn | Build to Earn |
|----------------|--------------|
| Experimentação, hipótese → tese | Produto estável, escalável |
| Drivado por produteiros, CMOs, designers | Drivado por engenharia |
| IA + não-técnicos suficientes | Precisa de engenheiro "de verdade" |
| Discovery real: ir pra produção, medir conversão | Entregar com qualidade para milhões |

Empresas precisarão de **plataforma de experimentação** que se funde com a camada sólida quando a hipótese é validada.

## Formação e educação

- Todo modelo educacional é pré-IA — precisa ser refeito
- Certificações (ex: AWS Professional) testam memorização que não será mais necessária
- Zarathon já reformulou todos os cursos de Prodops para modelo "guiado por AI"
- Juniores: "sem perspectiva de como virar nessa era"
- Resgate da literatura de análise de requisitos (caiu em desuso com ágil)

## Papéis em transformação

- EM + PM podem se fundir em "manager de tecnologia"
- Líder técnico: mais professor/guide + mais conhecedor do negócio
- Profissional T-shape: "saber o que precisa ter em cada fase" para validar output da IA
- Non-techs produzindo internal tools: liberando engenheiros para "software de verdade"

## Engenharia de software de 2030

> "Vai ser totalmente diferente da de 2020. A gente vai olhar pra 2020 e dizer: 'a gente fazia software desse jeito?'"

Comparação: deploy via disquete (2001) → CI/CD (2020) → ??? (2030).

## Relação com outros conceitos da wiki

- [[wiki/concepts/tres-camadas-coding-ia]] — reforça camada 3 como diferencial
- [[wiki/concepts/tdd-como-especificacao]] — TDD como checkpoint obrigatório
- [[wiki/concepts/code-review-como-portao]] — code review como "fase mais importante"
- [[wiki/concepts/automation-complacency]] — viés da eloquência + viés da automação
- [[wiki/concepts/sensores-computacionais]] — checkpoints determinísticos se consolidando
- [[wiki/concepts/multimodelo-slm]] — multimodelo para EVAL, não pode usar mesmo modelo
- [[wiki/concepts/formacao-novos-engenheiros]] — todo modelo educacional precisa ser refeito
- [[wiki/concepts/spec-driven-development]] — "20+ frameworks competindo, tudo muito mole ainda"
- [[wiki/concepts/harness-engineering]] — "todo mundo procurando um método"

## Referências

- [[raw/clippings/Boardroom 2606-01 - O Mercado de Tecnologia Mudou]]
- Canal Prodops (YouTube)
- zaratips.substack.com
