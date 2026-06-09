---
title: "As 3 camadas do coding com IA: onde o engenheiro de verdade ainda faz diferença"
type: source
tags: [harness-engineering, coding-com-ia, engenharia-de-software, camada-3]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[raw/clippings/As 3 camadas do coding com IA onde o engenheiro de verdade ainda faz diferença]]"]
author: "Zarathon Viana"
published: 2026-04-21
---

# As 3 camadas do coding com IA

## Resumo

Artigo fundador da série que propõe um modelo de 3 camadas para entender o coding com IA:

- **Camada 1 (Modelo):** controle baixo — você escolhe o modelo mas não o controla. Alerta sobre subsídio econômico insustentável dos providers.
- **Camada 2 (Ferramenta):** controle médio — você configura e estende (CLAUDE.md, .cursorrules, MCPs, hooks, skills). Aqui mora o Harness Engineering na definição da literatura.
- **Camada 3 (Engenharia de Software):** controle alto — TDD, linters, análise estática, type checking, arquitetura explícita, CI/CD com gates duros. É onde o engenheiro se destaca.

## Tese Central

> "Quanto mais próximo do modelo, menos controle você tem. Quanto mais próximo da engenharia de software clássica, mais controle você tem."

A camada 3 é investment capital. As outras duas são running cost.

## Dados-chave

- Estudo METR: devs seniores ficaram 19% mais lentos com IA, mas achavam que estavam 20% mais rápidos (diferença de 43 pontos percentuais)
- DORA 2025: "A IA não conserta um time; ela amplifica o que já está lá"
- 90% dos respondentes DORA reportam uso de IA; 30% reportam pouca/nenhuma confiança no código gerado
- Alerta econômico: OpenAI gastou ~8,67 bi em inferência nos primeiros 9 meses de 2025; Anthropic teve margem bruta negativa de 94% em 2024

## Ferramentas Mencionadas

- [[wiki/entities/claude-code]] — agentic-first, terminal
- [[wiki/entities/cursor]] — editor-first, inline
- [[wiki/entities/github-copilot]] — autocomplete-first
- [[wiki/entities/codex-openai]] — agent-first, isolado
- [[wiki/entities/opencode]] — open-source, agnóstico de provider
- Pi — minimalista, 4 ferramentas built-in

## Conceitos Relacionados

- [[wiki/concepts/harness-engineering]]
- [[wiki/concepts/tres-camadas-coding-ia]]
- [[wiki/concepts/sensores-computacionais]]

## Referências

- METR (2025): https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/
- DORA 2025: https://dora.dev/dora-report-2025/
- Fowler & Böckeler (2026): https://martinfowler.com/articles/harness-engineering.html
- LangChain (2026): https://www.langchain.com/blog/the-anatomy-of-an-agent-harness
