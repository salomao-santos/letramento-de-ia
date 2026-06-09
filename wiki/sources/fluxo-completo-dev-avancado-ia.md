---
title: "Meu fluxo COMPLETO de desenvolvimento avançado com IA"
type: source
tags: [waldemar-neto, workflow, cursor, paralelização, contexto, rpi, skills, mcp]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[raw/clippings/Meu fluxo COMPLETO de desenvolvimento avançado com IA]]"]
---

# Meu fluxo COMPLETO de desenvolvimento avançado com IA — Waldemar Neto

## Metadados

- **Autor:** [[wiki/entities/waldemar-neto|Waldemar Neto]] (Tech Leads Clube)
- **Formato:** Vídeo YouTube (~22min)
- **Data:** 2025-01-25
- **URL:** https://www.youtube.com/watch?v=-jPYunHFGL4

## Resumo

Demonstração prática end-to-end de como desenvolver uma funcionalidade complexa (integração Stripe) usando IA como executor. Mostra o setup mínimo necessário (rules, skills, MCPs, documentação), o fluxo completo de discovery → tasks → planos → implementação, e técnicas de paralelização com worktrees do Git.

## Pontos-chave

### 1. Fonte do contexto: Design Docs

Tudo começa com um design doc (pode ser RFC, ADR, PRD). Esse documento é a **fonte da verdade escrita e revisada por humanos**. A partir dele, a IA enriquece e gera código.

- Se o time já escreve RFCs/ADRs/design docs, está em ótimo lugar
- O design doc define: o que será feito, APIs envolvidas, escopo do MVP, itens definidos vs indefinidos
- A IA avalia o design doc e identifica lacunas antes de codar

### 2. Setup mínimo do repositório

Para ter alta efetividade com IA, o repo precisa de:

**Rules (ou agents.md):**
- Estrutura básica do projeto (always-on)
- Referências para documentações específicas (on-demand via progressive disclosure)
- "Se envolve módulos → usa X. Se envolve banco → usa Y. Se envolve controllers → usa Z."

**Skills:**
- Contexto especializado e reutilizável para tarefas repetitivas
- Exemplo: skill Confluence (sabe a instância, usa MCP Atlassian), skill Jira (cria/busca tasks)
- Evita repetir prompts toda vez

**MCPs:**
- Atlassian — acesso remoto a Confluence/Jira
- Context7 — documentação atualizada de libs
- MCP = protocolo para conhecimento remoto; Skill = tática local

**Documentação (docs/):**
- Architecture overview
- Padrões de código do projeto
- Padrões de modularização
- Evolui com o tempo — cada plano que falha revela lacuna a documentar

### 3. Fluxo operacional (RPI na prática)

1. **IA avalia design doc** — identifica o que está definido e o que falta
2. **Quebra em tasks** — cada "fase" vira uma task (não tasks micro como para humano)
3. **Cria tasks no Jira** — via skill dedicada
4. **Avalia paralelização** — IA identifica dependências e sugere o que pode rodar em paralelo
5. **Abre novo contexto** — manter janela baixa (máx 30% de 200K tokens)
6. **Cria plano para task** — no modo plan, usando modelo inteligente (Claude Sonnet)
7. **Executa plano em novo agente** — com modelo mais barato (Cursor Composer) para execução pura de steps
8. **Revisa e aprova** — revisão humana do resultado

### 4. Gestão de janela de contexto

- Ao chegar em ~44% da janela, abrir novo contexto — risco de alucinação aumenta
- Meta: manter ≤30% em janela de 200K tokens
- Separar planeamento (modelo caro) de execução (modelo barato, contexto limpo)
- Quanto maior o projeto, mais pesquisa o agente faz → mais consome contexto

### 5. Paralelização com Git Worktrees

- Worktrees permitem trabalhar em branches paralelas sem conflitar
- Enquanto um agente implementa task principal, outro resolve bug em worktree separada
- Fluxo: criar branch → implementar → review → apply de volta na branch principal → commit
- Possível rodar 2-3 agentes simultâneos (custo financeiro é o limite)
- "Cereja do bolo": aproveitar tempo de espera para iniciar outras tasks

### 6. Estratégia de modelos

- **Modelo inteligente (Claude Sonnet):** para Research e Plan — precisa raciocinar
- **Modelo barato (Cursor Composer):** para Implement — execução de steps definidos, mais rápido e econômico

### 7. Documentação como investimento incremental

- Cada plano que falta algo → melhorar documentação
- Estado ideal ("Nirvana"): IA faz tudo sem ajustes
- Leva dias para construir bom contexto, mas o retorno é exponencial
- "Não é muita documentação — são as coisas que não são normais, específicas do projeto"

## Contribuições novas para a wiki

- **Demonstração prática de RPI** complementando o guia teórico anterior ([[wiki/sources/spec-driven-guia-completo-waldemar]])
- **Worktrees como vetor de paralelização** — conceito novo nesta wiki
- **Regra 30%:** meta operacional de uso de janela de contexto (complementa a regra ≤200K)
- **Padrão de delegação de plano:** modelo caro planeja, modelo barato executa
- **Skills como automação de workflow:** skill Confluence + skill Jira eliminam prompts repetitivos
- **Diferença clara MCP vs Skill vs Docs:** remoto vs local tático vs local persistente

## Relações

- Operacionaliza: [[wiki/concepts/spec-driven-development]] (workflow RPI na prática)
- Demonstra: [[wiki/concepts/compaction-de-contexto]] (gestão ativa de janela)
- Aplica: [[wiki/concepts/harness-engineering]] (rules + skills + MCPs + docs como outer harness)
- Complementa: [[wiki/sources/spec-driven-guia-completo-waldemar]] (parte prática do vídeo teórico)
- Usa: [[wiki/entities/cursor]] como ferramenta principal

## Referências

- [[raw/clippings/Meu fluxo COMPLETO de desenvolvimento avançado com IA]]
- [[wiki/entities/waldemar-neto]]
- [[wiki/concepts/compaction-de-contexto]]
- [[wiki/concepts/harness-engineering]]
- [[wiki/concepts/spec-driven-development]]
