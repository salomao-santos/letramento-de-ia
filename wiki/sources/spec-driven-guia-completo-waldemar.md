---
title: "Spec-Driven Development: A Habilidade #1 para Devs de 2026 (Guia Completo)"
type: source
tags: [spec-driven-development, context-engineering, rpi, subagents, workflow]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[raw/clippings/Spec-Driven Development - A Habilidade 1 para Devs de 2026 (Guia Completo)]]"]
---

# Spec-Driven Development: A Habilidade #1 para Devs de 2026 (Guia Completo)

## Metadados

- **Autor:** [[wiki/entities/waldemar-neto|Waldemar Neto]]
- **Canal:** YouTube (Tech Leads Clube)
- **Data:** 2025-05-01
- **Duração:** ~12 min
- **URL:** https://www.youtube.com/watch?v=YFDp-smGYqQ

## Resumo

Guia prático e tutorial de Spec-Driven Development, mostrando como aplicar o padrão em qualquer code agent. O vídeo complementa o outro vídeo do mesmo autor que critica as limitações do SDD — aqui o foco é operacionalização positiva do workflow.

## Tese central

O que separa resultado medíocre de um sistema completo e funcional é o **contexto** que tu dá pro agente. Spec Driven Development é um padrão para otimizar esse contexto e escalar implementações sem explodir a janela.

## Conceitos-chave

### RPI — Research, Plan, Implement

Framework de 3 fases para desenvolvimento com agentes:

1. **Research:** abrir janela de contexto dedicada, navegar codebase, consultar MCPs, ler documentação. Objetivo: descobrir o que precisa fazer.
2. **Plan:** salvar tudo que aprendeu em arquivos Markdown (spec, design, tasks). Preserva conhecimento sem gastar tokens futuros.
3. **Implement:** executar tasks numa janela limpa, referenciando apenas os markdowns criados na fase de plan.

> Premissa: separar research de implementação em janelas diferentes evita poluição de contexto e economiza tokens.

### Otimização da janela de contexto

- Janelas de 1M tokens existem, mas recomenda ficar em **~200K tokens** — quanto maior, mais chance de alucinação
- O que entra na janela: prompt + arquivos relevantes + agents.md/rules + MCPs necessários + skills necessárias
- Caso real: funcionalidade que mudou **90 arquivos** com janela de apenas **50K tokens** (graças ao RPI + subagents)

### Anatomia de uma Spec

1. **Problema:** o que está errado/faltando
2. **Goals:** métricas ou resultados esperados
3. **Fora de escopo:** o que deliberadamente não entra
4. **User stories:** quais problemas de usuário resolve

### Design (opcional)

- Diagrama de arquitetura da solução
- Componentes necessários no alto nível
- O que será reusado
- Decisões importantes

Justificativa para separar design das tasks: num projeto com ~40 tasks, manter design dentro de cada task gera repetição. Design vive em arquivo separado, referenciável de qualquer task.

### Tasks — breakdown otimizado

Cada task contém:
- O que vai ser feito
- Onde vai ser feito
- O que vai ser reusado
- Pré-requisitos (dependências com outras tasks)
- Definition of Done

Propriedades do breakdown:
- Tasks sequenciais vs paralelizáveis explicitamente marcadas
- Cada task é autocontida — agente não precisa fazer nova pesquisa
- Tamanho otimizado para assertividade (escopo pequeno = menos erro)

### Subagents para paralelização

- Na fase de implementação, o agente principal abre subagents para tasks paralelas
- Exemplo real: 4 subagents simultâneos, cada um trabalhando em tasks independentes
- Benefícios: otimiza contexto (cada subagent tem janela própria), menos chance de erro, escala de implementação

### Estado (state)

Arquivo que guarda decisões importantes tomadas durante a implementação. Permite:
- Continuidade entre sessões (abrir nova janela e dizer "continua o projeto X")
- Commitar specs e retomar depois
- Separar em vários PRs
- Rastreabilidade de decisões

## Ferramentas mencionadas

- **TLC Spec Driven** (Tech Leads Clube / Felipe Rodrigues): skill principal demonstrada, flexível, instalação global
- **Spec Kit** (GitHub): alternativa mais engessada, mesmos princípios
- Code agents usados: [[wiki/entities/claude-code|Claude Code]], [[wiki/entities/cursor|Cursor]], [[wiki/entities/github-copilot|GitHub Copilot]]

## Workflow resumido

```
1. Dar contexto (PRD, requisito, conversa)
     ↓
2. Skill cria: Spec → Design (opcional) → Tasks
     ↓
3. Abrir NOVA janela limpa
     ↓
4. Executar tasks (com subagents para paralelização)
     ↓
5. Estado salva decisões para continuidade
```

## Dicas práticas

- Instalar skill global — funciona em qualquer projeto
- Para projetos pequenos, pular design (só spec + tasks)
- Para projetos grandes, usar todas as fases
- Sempre abrir nova janela para implementação (contexto limpo)
- Pedir para o agente usar subagents ao máximo na execução

## Relação com outras fontes

- **Complementar a** [[wiki/sources/spec-driven-limite-harness-proximo-passo]]: aquele critica limitações, este operacionaliza
- **Implementa** o princípio de [[wiki/concepts/compaction-de-contexto|Clear > Compact]] na prática (nova janela = contexto limpo)
- **Alinhado com** [[wiki/sources/full-walkthrough-workflow-ai-coding]]: mesma lógica de vertical slices e tickets pequenos
- **Confirma** a crítica da [[wiki/sources/software-fundamentals-matter-more-than-ever]]: spec sozinha não basta se não há design consciente

## Referências

- [[raw/clippings/Spec-Driven Development - A Habilidade 1 para Devs de 2026 (Guia Completo)]]
- [[wiki/concepts/spec-driven-development]]
- [[wiki/concepts/compaction-de-contexto]]
- [[wiki/entities/waldemar-neto]]
