---
title: "Rules, Skills, MCPs e Subagents — DOMINE os principais conceitos de IA para ganhar PRODUTIVIDADE"
type: source
tags: [waldemar-neto, felipe-rodrigues, skills, rules, mcp, subagents, contexto, progressive-disclosure, tech-leads-clube]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[raw/clippings/Rules, Skills, MCPs e Subagents - DOMINE os principais conceitos de IA para ganhar PRODUTIVIDADE]]"]
---

# Rules, Skills, MCPs e Subagents — Waldemar Neto & Felipe Rodrigues

## Metadados

- **Autores:** [[wiki/entities/waldemar-neto|Waldemar Neto]] e [[wiki/entities/felipe-rodrigues|Felipe Rodrigues]] (Tech Leads Clube)
- **Formato:** Live/Aula YouTube (~45min)
- **Data:** 2025-02-07
- **URL:** https://www.youtube.com/watch?v=omkEi4GTCj8

## Resumo

Aula completa cobrindo os 4 pilares de produtividade com IA: Rules, Skills, MCPs e Sub Agents. Mostra a evolução histórica (2023→2025), explica por que custom sub agents estão morrendo em favor de skills + sub agents genéricos, e demonstra um fluxo real integrando Jira + skills + sub agents genéricos em paralelo. No final, apresenta uma biblioteca open-source de skills curadas do Tech Leads Clube.

## Pontos-chave

### 1. Evolução histórica dos fluxos agênticos

| Período | Marco | Problema/Avanço |
|---------|-------|-----------------|
| 2022-2023 | ChatGPT3, janelas maiores (128-200K) | Começou uso pesado para codebase |
| 2023-2024 | MCPs (Anthropic) | Buscar dados externos; contexto inflou |
| 2024-2025 | Planos + Progressive Disclosure | Janela menor, busca sob demanda |
| 2025 | Skills + Sub agents genéricos | Capacidades portáveis, paralelização sem custom agents |

### 2. O problema do contexto inflado

Antes (2024): instruções + MCPs + regras + documentação + workflows — tudo junto, tudo carregava ao mesmo tempo. Resultado: prompt gigante, janela de contexto explodida, alucinação, gasto excessivo de tokens.

**Regra operacional:** o ideal numa janela de 200K tokens é ter no máximo **40% da janela ocupada**. A partir disso, respostas perdem precisão.

### 3. Progressive Disclosure

Conceito-chave da evolução 2025: a IA descobrindo automaticamente o que precisa e carregando sob demanda.

- Antes: todos os MCPs ficavam na memória do agente desde o início
- Agora: agente sabe que precisa de um MCP específico, vai lá e carrega (ex: search tool da Anthropic)
- Skills carregam só o front matter; corpo carrega quando invocada
- Rules podem ser always-on ou sob demanda

### 4. Rules e agents.md (estáticos)

**Rules** = guidelines estáticos carregados no início. Conteúdo:
- Estilo de código, convenção do projeto, estrutura
- Estrutura de alto nível do projeto
- Referências para onde buscar mais documentação

**agents.md** = mesmo efeito, padrão de indústria. Máximo ~200 linhas. Só estrutura + ponteiros para docs.

**Princípio:** "Se ele precisa de entendimento, é coisa estática: agents.md e rules."

### 5. Skills (capabilities portáveis)

Skills são habilidades encapsuladas e reutilizáveis. Diferem de sub agents porque:
- Rodam no contexto do agente que as invoca (não isolam contexto)
- São portáveis entre projetos e IDEs
- Carregam sob demanda (agente lê front matter → invoca quando precisa)
- Substituem o caso de uso mais comum de custom sub agents

**Exemplos concretos:**
- Jira assistant (busca/cria tasks com instância pré-configurada)
- Confluence (busca/cria páginas)
- Testes end-to-end (com exemplos pré-definidos)
- Análise de módulos de domínio
- Spec-driven development (simplificação do spec-kit)

**Por que skill ao invés de MCP direto?** A skill abstrai a instrumentação: já sabe a instância, o projeto, o board. Sem skill, cada prompt precisa repetir URLs, tokens, contexto. Skill = abstração de chamada de API.

**Criação é simples:** faça algo manualmente uma vez → peça à IA: "a partir do que conversamos, cria uma skill".

### 6. MCPs (conexão externa)

MCP = protocolo para buscar/inserir/atualizar dados externos. Interface para falar com o mundo externo e trazer contexto para dentro.

- Criado pela Anthropic, adotado como padrão de indústria
- Serve para coisas dinâmicas (conteúdo que muda frequentemente)
- Não só leitura: também insere comentários, cria PRs, documenta no Confluence
- Se carregar IDE com muitos MCPs (empresa grande) → lento. Skill é melhor para conhecimento estável.

### 7. Sub Agents: de custom para genérico

**Antes (até set/2024):** pessoas criavam custom sub agents com 2000-4000 linhas para:
- Ter algo especializado (criar teste, fazer release, criar PDF)
- Rodar em processo separado

**Problema:** consumia metade do contexto só para iniciar; empilhar sub agents = custo multiplicado.

**Mudança da indústria:** separar dois conceitos que estavam misturados:
- **Capability** (habilidade) → virou **Skill**
- **Processo isolado** (paralelização, contexto limpo) → virou **Sub Agent Genérico**

**Sub agents genéricos** (Cursor, Claude Code):
- Propósito genérico — não precisam de configuração custom
- Recebem parte do contexto, buscam skills necessárias, retornam output mínimo
- Paralelizáveis: "analyze these 3 modules in parallel"
- Mantêm janela do agente principal baixa

### 8. Migração real: Felipe mostrou como quebrou um sub agent de ~2000 linhas em múltiplas skills de ~66 linhas cada

Skills resultantes: core standards, create component, form, integrate API. Cada skill com front matter descritivo ("use when task mentions schemas validation field arrays disabled states") — agente invoca automaticamente.

### 9. Diferença conceitual Agent vs Skill

- **Agent** = chapéu/papel que o agente veste (testador, code reviewer, documentador)
- **Skill** = instrução para executar tarefa, independente do papel. Pode ser usada por qualquer agent.

### 10. Gasto de tokens: investimento com ROI

Gastar mais planejando (rules, guidelines, skills) = menos token de retrabalho, bug, código duplicado, alucinação. É investimento com retorno no ciclo completo de desenvolvimento.

### 11. Centralização em times

- Empresas centralizam conhecimento + usam MCP para acessar
- Se não muda com frequência → marketplace interno de skills (release versionada)
- Se muda frequentemente / vem de banco de dados → MCP é melhor
- Centenas de MCPs numa empresa grande → lento; skills locais são mais eficientes

### 12. Biblioteca de Skills do Tech Leads Clube

Repositório open-source com skills curadas e testadas. Features:
- Detecta IDEs instaladas na máquina
- Instala via symlink (auto-atualiza) ou cópia
- Skills com max 500 linhas (recomendação Anthropic)
- Inclui skill de Spec Driven Development (simplificação do spec-kit GitHub)

## Contribuições novas para a wiki

- **Progressive Disclosure como padrão formal:** IA descobre e carrega contexto sob demanda (não tudo de uma vez)
- **Morte dos custom sub agents:** skill para capability, sub agent genérico para isolamento de contexto
- **Regra 40%:** complementa a regra 30% do vídeo anterior — a partir de 40% da janela, precisão cai
- **Separação clara Agent (papel) vs Skill (habilidade):** taxonomia formal
- **Migração concreta:** sub agent ~2000 linhas → múltiplas skills ~66 linhas (caso Felipe)
- **Marketplace de skills como padrão de empresa:** versionado, local, sem custo de MCP
- **Felipe Rodrigues:** co-host, demonstra práticas concretas de migração e criação de skills

## Relações

- Complementa: [[wiki/sources/fluxo-completo-dev-avancado-ia]] (setup mínimo → aqui aprofunda cada componente)
- Complementa: [[wiki/sources/spec-driven-guia-completo-waldemar]] (RPI → aqui explica skills e sub agents por trás)
- Demonstra: [[wiki/concepts/compaction-de-contexto]] (progressive disclosure como otimização ativa)
- Expande: [[wiki/concepts/harness-engineering]] (outer harness: rules + skills + MCPs como taxonomia completa)
- Evolui: [[wiki/concepts/spec-driven-development]] (skills como portadora de capabilities antes em sub agents)

## Referências

- [[raw/clippings/Rules, Skills, MCPs e Subagents - DOMINE os principais conceitos de IA para ganhar PRODUTIVIDADE]]
- [[wiki/entities/waldemar-neto]]
- [[wiki/entities/felipe-rodrigues]]
- [[wiki/concepts/compaction-de-contexto]]
- [[wiki/concepts/harness-engineering]]
