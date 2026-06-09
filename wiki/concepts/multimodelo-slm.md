---
title: "Multimodelo e SLMs"
type: concept
tags: [modelos, custo, slm, infraestrutura, futuro]
created: 2026-06-08
updated: 2026-06-09
sources: ["[[wiki/sources/engenharia-era-piloto-automatico]]", "[[wiki/sources/boardroom-mercado-tecnologia-mudou]]"]
---

# Multimodelo e SLMs (Specific Language Models)

## Conceito

Visão de futuro onde equipes de engenharia operam com múltiplos modelos de IA, selecionando o mais adequado por tarefa em vez de depender de um único LLM genérico e caro.

## De LLM para SLM

| Fase | Horizonte | Estratégia |
|------|-----------|-----------|
| Atual | Agora | LLMs subsidiados (Sonnet, GPT, Gemini) |
| Transição | 1-2 anos | Híbrido: LLM caro para raciocínio + open models para implementação |
| Futuro | 5-10 anos | SLMs específicos por domínio, rodando localmente (~200MB) |

**SLM = Specific Language Model** (ou Small Language Model): modelo fine-tunado para um domínio específico, pequeno o suficiente para rodar na máquina local.

## Motivação econômica

- Modelos atuais são subsidiados (Anthropic com margem bruta negativa de 94%)
- Custos devem subir ~10x quando subsídios acabarem
- Modelos open source (Qwen, DeepSeek) já entregam resultados comparáveis para implementação
- Empresas poderão criar e distribuir SLMs internos

## Workflow multimodelo na prática

Exemplo do Zarathon/Matos:
- **Raciocínio/Design:** Opus, Gemini Pro Thinking (modelos caros)
- **Implementação:** Qwen 2.6, DeepSeek V4 (modelos baratos/open)

> "Não tem porque eu gastar cinco vezes mais com Sonnet se eu posso usar 1/5 desse valor com Qwen para a mesma tarefa."

## Experimentação com SLMs

Zarathon testou fine-tune de Qwen 2.5 para código Go:
- Modelo de ~200MB
- Roda local
- Resultados promissores (ainda precisa refinar)

## Implicações para engenheiros

- Aprender a navegar custo vs capacidade por tarefa
- Não travar workflow num único provider
- Entender qual tipo de tarefa precisa de raciocínio profundo vs geração mecânica
- Multiagente + multimodelo = orquestração de especialistas

## Ver também

- [[wiki/concepts/tres-camadas-coding-ia]] — Camada 1 (Modelo) é onde essa escolha acontece
- [[wiki/sources/engenharia-era-piloto-automatico]]
- [[wiki/sources/boardroom-mercado-tecnologia-mudou]] — multimodelo para EVAL; não pode usar mesmo modelo julgando a si mesmo ("ecos")
