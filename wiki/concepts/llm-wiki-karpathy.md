---
title: "LLM Wiki (Padrão Karpathy)"
type: concept
tags: [memoria, wiki, knowledge-management, karpathy, compilacao]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[wiki/sources/memoria-agentes-karpathy-agentmemory]]"]
---

# LLM Wiki (Padrão Karpathy)

## Definição

Arquitetura de gestão de conhecimento proposta por [[wiki/entities/andrej-karpathy|Andrej Karpathy]] (abril 2026) onde um LLM **compila** conhecimento incrementalmente em páginas markdown interligadas, em vez de **recuperar** sob demanda (RAG).

## Insight central

> Conhecimento deve ser compilado, não re-derivado a cada query.

RAG tradicional redescobre respostas partindo dos documentos brutos a cada pergunta. A LLM Wiki sintetiza uma vez, e queries posteriores partem da síntese. Isso cria **efeito composto**: cada ingestão enriquece o todo.

## Arquitetura — 3 Camadas

```
┌─────────────────────────────────┐
│          Schema Layer           │  ← Convenções, taxonomia, CLAUDE.md
├─────────────────────────────────┤
│          Wiki Layer             │  ← Páginas MD geradas pelo LLM
├─────────────────────────────────┤
│        Raw Sources              │  ← Documentos imutáveis (source of truth)
└─────────────────────────────────┘
```

1. **Raw Sources** — papers, artigos, transcrições, notas. Imutáveis. Fonte da verdade.
2. **Wiki Layer** — páginas markdown geradas e mantidas pelo LLM. Cada conceito = uma página. Páginas se referenciam. O LLM atualiza, faz cross-reference, marca contradições.
3. **Schema** — arquivo que define convenções (nomenclatura, taxonomia, estrutura mínima de cada entrada).

## Operações — 3 Verbos

### Ingest
Fonte nova chega → LLM lê → extrai o que importa → atualiza 10-15 páginas existentes → cria as que faltam → conserta cross-references.

### Query
Pergunta → resposta sintetizada com citações → insights valiosos viram páginas novas.

### Lint
Passes periódicos → detecta contradições → claims desatualizadas → conexões faltando.

## Por que funciona agora

Wikis humanas morrem porque o trabalho de manutenção é tedioso. LLMs são bons justamente em escrita e manutenção repetitiva. A aposta: finalmente existe uma "máquina" que faz o trabalho chato de manter a wiki viva.

## Vantagem sobre RAG

| Aspecto | RAG | LLM Wiki |
|---------|-----|----------|
| Processamento | Re-derive a cada query | Sintetiza uma vez, queries partem da síntese |
| Conhecimento | Estático nos chunks | Compõe ao longo do tempo |
| Cross-referência | Não existe | Explícita (wikilinks) |
| Contradições | Invisíveis | Marcadas explicitamente |
| Custo por query | Alto (retrieval + geração) | Baixo (leitura de página pronta) |

## Implementações

- **Manual:** diretório `.docs/` ou `docs/` com markdown + arquivo MEMORY.md listando tópicos
- **Este vault:** segue exatamente o padrão (raw/ → wiki/ → .kiro/steering/)
- **[[wiki/entities/agentmemory|agentmemory]]:** automatiza ingest/query/lint via MCP, adiciona consolidação em tiers e retrieval híbrida

## Relação com outros conceitos

- Resolve o problema criado pela [[wiki/concepts/compaction-de-contexto|compaction de contexto]]
- É a camada 3 do modelo de 4 camadas para [[wiki/concepts/memoria-longo-prazo-agentes|memória de longo prazo]]
- Alinha com [[wiki/concepts/harness-engineering]]: a wiki é um "guide" que canaliza o agente

## Referências

- Gist original: Karpathy, abril 2026
- Artigo VentureBeat: "Karpathy shares LLM knowledge base architecture that bypasses RAG"
- [[wiki/sources/memoria-agentes-karpathy-agentmemory]]
