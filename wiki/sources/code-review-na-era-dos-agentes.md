---
title: "Se teu code review é LGTM automático, o gargalo é tu, não o agente"
type: source
tags: [code-review, lgtm, ferramentas-review, pr-size, coding-com-ia]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[raw/clippings/Se teu code review é LGTM automático, o gargalo é tu, não o agente]]"]
author: "Zarathon Viana"
published: 2026-04-09
---

# Code review na era dos agentes

## Resumo

Quarto artigo da série. Fecha o bloco dos 3 pilares da camada 3: arquitetura (por onde), teste (o que), e agora code review (se pode passar). O LGTM automático sempre foi fraude, mas antes era barata — agora o agente erra em volume industrial e com cara de certo.

## Tese Central

> "Se você não consegue descrever como seria o erro, você não está revisando, está carimbando."

## Conceitos-chave

### O inimigo novo: "quase certo"
- 66% dos devs (Stack Overflow 2025): maior frustração = soluções de IA "quase certas"
- 45% dizem que depurar código de IA consome mais tempo
- O LLM gera código plausível fazendo a coisa errada com elegância

### Checklist novo para code review
O que SÓ humano revisa:
- Alucinação de API (método que não existe, lib inventada)
- Lógica de negócio plausível mas errada
- Edge cases mal-entendidos
- Acoplamento que parece local mas quebra o sistema
- Decisão de design que não cabe na arquitetura

### Anti-padrões amplificados pela IA
- **Bikeshedding**: debate estilo enquanto lógica errada passa
- **Review de estilo**: trabalho do linter feito na mão
- **Carimbo apressado**: scope insensitivity — mesmo esforço em 100 e 1000 linhas
- **Viés de automação**: conselho automatizado errado seguido a taxa 26% maior (Goddard et al., 2012)

### PR pequeno como ferramenta anti-LLM
- Eficácia do review desaba após 200-400 linhas (SmartBear/Cisco)
- Detecção: ~87% em PRs < 100 linhas → ~28% em PRs > 1000 linhas
- Disciplina: 200-400 linhas por PR, um propósito por PR

### Agente revisando agente: câmara de eco
- "Homogenisation trap": erros correlacionados ecoam em vez de se cancelar
- Revisor de IA é SENSOR, não juiz
- IA antes, humano por último = fluxo ideal

### Ferramentas de AI code review
- **CodeRabbit**: 2M+ repos, 13M+ PRs; baseado em diff (ponto fraco: não vê contexto global)
- **Greptile**: indexa repo inteiro; benchmarks variam (24% a 82% dependendo da fonte)
- **Copilot Code Review**: adoção explosiva por zero fricção no GitHub
- Melhores ferramentas: 42-48% de detecção de bug real (benchmark Macroscope)

### Conventional Commits + Semantic Release
- Commit semântico = contrato legível para volume industrial de mudanças
- Permite rollback rápido e changelog automático

## O fluxo que funciona
1. Código sobe
2. CI roda gates duros (lint, tipo, teste, coverage)
3. IA faz primeira passada (sensor)
4. Autor corrige achados da IA
5. Humano revisa o que importa (juiz)

## Dados-chave
- Pesquisa Código Fonte TV 2025: 95,5% dos devs brasileiros usam IA
- Code Complete: revisão detecta 55-60% dos defeitos
- Defeito em produção: 10x a 100x mais caro que pego em review
- Stripe/Shopify: -30% a -40% idas e vindas com fluxo IA→humano

## Conceitos Relacionados
- [[wiki/concepts/tres-camadas-coding-ia]]
- [[wiki/concepts/sensores-computacionais]]
- [[wiki/concepts/automation-complacency]]
- [[wiki/concepts/code-review-como-portao]]

## Referências
- Stack Overflow Survey 2025: https://survey.stackoverflow.co/2025/
- Pesquisa Código Fonte TV 2025: https://pesquisa.codigofonte.com.br/2025
- SmartBear/Cisco: https://smartbear.com/learn/code-review/best-practices-for-peer-code-review/
- Goddard et al. (2012): Systematic review on automation bias
- CodeRabbit: https://www.coderabbit.ai/
