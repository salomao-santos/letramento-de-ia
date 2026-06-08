---
title: "Understanding Spec-Driven-Development: Kiro, spec-kit, and Tessl"
type: source
tags: [spec-driven-development, kiro, spec-kit, tessl, workflows]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[raw/clippings/Understanding Spec-Driven-Development Kiro, spec-kit, and Tessl]]"]
author: "Birgitta Böckeler"
published: 2026-06-08
---

# Spec-Driven Development: Kiro, spec-kit e Tessl

## Resumo

Artigo da Birgitta Böckeler que analisa o conceito emergente de "Spec-Driven Development" (SDD) e compara três ferramentas que se rotulam como implementações dele: Kiro (AWS), spec-kit (GitHub) e Tessl Framework. Oferece análise crítica sobre limitações e questões em aberto.

## Definição de SDD

Escrever uma "spec" antes de escrever código com IA ("documentation first"). A spec se torna a fonte da verdade para humano e IA.

## Três Níveis de SDD

| Nível | Descrição | Manutenção da spec |
|-------|-----------|-------------------|
| **Spec-first** | Spec escrita antes, usada para a task | Spec descartada após task |
| **Spec-anchored** | Spec mantida para evolução da feature | Spec editada ao longo do tempo |
| **Spec-as-source** | Spec é o artefato principal, humano nunca toca no código | Código gerado da spec continuamente |

## As Ferramentas

### Kiro (AWS)
- Mais leve das três
- Workflow: Requirements → Design → Tasks
- Cada step = 1 arquivo markdown
- Requirements: User Stories com acceptance criteria (GIVEN/WHEN/THEN)
- Memory bank chamado "steering" (product.md, tech.md, structure.md)
- Atualmente spec-first apenas (sem spec-anchored claro)

### spec-kit (GitHub)
- CLI que configura workspace para vários assistentes
- Workflow: Constitution → Specify → Plan → Tasks
- Constitution = rules file poderoso (princípios imutáveis)
- Checklists como "definition of done" para cada step
- Cria MUITOS arquivos markdown para review
- Aspira spec-anchored mas na prática é spec-first (cria branch por spec)

### Tessl Framework (beta privado)
- CLI + MCP server
- Único que aspira explicitamente spec-anchored e spec-as-source
- Mapeamento 1:1 entre spec e arquivo de código
- Código marcado com `// GENERATED FROM SPEC - DO NOT EDIT`
- Specs em nível baixo de abstração (por arquivo de código)
- Comando `tessl build` gera código a partir da spec

## Observações Críticas

### Um workflow para todos os tamanhos?
- Kiro: para um bug pequeno, gerou 4 user stories com 16 acceptance criteria = sledgehammer para crack a nut
- spec-kit: para uma feature de 3-5 pontos, criou tantos arquivos que seria mais rápido codar direto

### Review de markdown vs review de código?
> "Honestamente, prefiro revisar código a todos esses arquivos markdown."

### Falsa sensação de controle?
- Agente frequentemente não segue todas as instruções mesmo com spec detalhada
- Context window maior ≠ IA vai absorver tudo que está lá
- Agente ignorou notas sobre classes existentes e recriou duplicatas

### Separação funcional vs técnica
- Confuso na prática saber quando ficar no nível funcional vs adicionar detalhes técnicos
- Profissão tem histórico ruim em separar requirements de implementação

### Paralelo com MDD (Model-Driven Development)
- Specs do Tessl lembram modelos MDD (DSLs customizadas → código gerado)
- MDD nunca decolou para business apps (abstração awkward, overhead)
- LLMs removem algumas restrições do MDD (não precisa de linguagem parseável, não precisa de code generator elaborado)
- Preço: não-determinismo
- Risco: inflexibilidade E não-determinismo ao mesmo tempo

### Verschlimmbesserung
> "Estamos piorando algo na tentativa de melhorar?" — Sobre workflows que criam overhead e amplificam desafios existentes como review overload e alucinações.

## Conclusão do artigo

O princípio geral de spec-first é valioso. Mas:
- O termo "SDD" ainda não é bem definido (já sofre semantic diffusion)
- Ferramentas tentam alimentar agentes com workflows existentes de forma literal demais
- Abordagens elaboradas com muitos arquivos podem ser Verschlimmbesserung

## Conceitos Relacionados

- [[wiki/concepts/harness-engineering]]
- [[wiki/concepts/tres-camadas-coding-ia]]
- [[wiki/entities/birgitta-bockeler]]
- [[wiki/entities/kiro-ide]]

## Referências

- Artigo original: https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html
- Kiro: https://kiro.dev/
- spec-kit: https://github.com/github/spec-kit
- Tessl: https://docs.tessl.io/
- GitHub blog sobre spec-kit: https://github.blog/ai-and-ml/generative-ai/spec-driven-development-with-ai-get-started-with-a-new-open-source-toolkit/
