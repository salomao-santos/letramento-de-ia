---
title: "Devs são os novos pilotos de avião (e ninguém tá te preparando pra isso)"
type: source
tags: [automação, habilidades-manuais, aviação, formação, degradação-de-skills]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[raw/clippings/Devs são os novos pilotos de avião (e ninguém tá te preparando pra isso)]]"]
author: "Zarathon Viana"
published: 2026-04-09
---

# Devs são os novos pilotos de avião

## Resumo

Artigo que traça um paralelo detalhado entre a automação na aviação e o uso de IA por desenvolvedores. Usa o caso do voo Air France 447 (2009) como metáfora central: quando o autopilot falha, só quem tem "horas de voo manual" consegue assumir.

## Tese Central

> "A pergunta que você deveria estar se fazendo não é 'quanto de IA eu uso?'. É 'quando foi a última vez que eu voei no manual?'"

## Conceitos-chave

### Ironias da Automação (Bainbridge, 1983)
"Ao tirar as partes fáceis do trabalho, a automação torna as partes difíceis ainda mais difíceis." Três consequências:
1. Perda de prática das habilidades manuais
2. Perda de consciência situacional
3. Incapacidade de retomar o controle quando automação falha

### Salto de determinístico para probabilístico
Pela primeira vez na história da engenharia de software, o salto de abstração não é determinístico→determinístico (Assembly→C→Java→Frameworks), mas determinístico→probabilístico (código→geração por LLM).

### Automation complacency
METR: devs ficaram 19% mais lentos com IA mas acharam que ficaram 20% mais rápidos. Diferença de percepção = complacência.

### Horas de voo para devs
Analogia com requisitos da ANAC (150h mínimas para Piloto Comercial; companhias pedem 500-5000h). Formas de acumular:
- Micro-SaaS e projetos próprios (voo solo)
- Contribuição open source (co-pilotagem)
- Freelance (voos curtos com risco real)
- Build in public
- Hackathons com produto real

### O piloto moderno
Usa automação na maior parte do voo, mas assume controle manual na decolagem e pouso (fases de maior risco). Para devs: arquitetura, design de sistemas distribuídos, investigação de bugs complexos = voo manual obrigatório.

## Dados-chave
- 84% dos devs usam IA no dia a dia (2026)
- 27-41% de todo código em produção é gerado por IA
- Estudo Stanford/ADP: emprego de devs 22-25 anos caiu ~20% desde pico de 2022
- Degradação de performance com automação: 61% (grupo automatizado) vs 31% (grupo manual)

## Conceitos Relacionados
- [[wiki/concepts/automation-complacency]]
- [[wiki/concepts/horas-de-voo-para-devs]]
- [[wiki/concepts/tres-camadas-coding-ia]]

## Referências
- Bainbridge (1983): "Ironies of Automation"
- METR (2025): https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/
- Stanford/ADP (2025): https://digitaleconomy.stanford.edu/wp-content/uploads/2025/08/Canaries_BrynjolfssonChandarChen.pdf
- Air France 447: https://humanfactors101.com/incidents/air-france-flight-447/
