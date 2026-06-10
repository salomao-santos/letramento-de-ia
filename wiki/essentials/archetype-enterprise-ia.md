---
title: "O Essencial ao Construir um Archetype para Projetos Enterprise com IA"
type: synthesis
tags: [archetype, service-template, harness-engineering, ambient-affordances, tdd, spec-driven, java, spring, python]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[wiki/sources/arquitetura-na-era-dos-agentes]]", "[[wiki/sources/maintainability-sensors]]", "[[wiki/sources/harness-engineering-fowler]]", "[[wiki/sources/tdd-na-era-dos-agentes]]", "[[wiki/sources/spec-driven-development]]", "[[wiki/sources/spec-driven-guia-completo-waldemar]]", "[[wiki/sources/code-review-na-era-dos-agentes]]", "[[wiki/sources/clean-architecture-custando-caro-era-ia]]", "[[wiki/sources/fluxo-completo-dev-avancado-ia]]", "[[wiki/sources/rules-skills-mcps-subagents-waldemar]]", "[[wiki/sources/software-fundamentals-matter-more-than-ever]]"]
---

# O Essencial ao Construir um Archetype para Projetos Enterprise com IA

Na era dos agentes, um archetype (service template) não é só código que compila — é um repositório com **cercas determinísticas já montadas**. O agente começa dentro de fronteiras claras em vez de um campo aberto.

Este artigo descreve o que um template enterprise precisa conter para ser governável por agentes de IA, com exemplos práticos em **Java + Spring** e **Python**.

---

## As 5 Camadas

Todo archetype governável responde a cinco perguntas sobre o trabalho do agente:

| # | Camada | Pergunta que responde |
|---|--------|-----------------------|
| 1 | **Estrutura** | Por onde o agente pode andar? |
| 2 | **Especificação** | O que ele deve produzir? |
| 3 | **Guides** | O que ele lê antes de agir? |
| 4 | **Sensors** | O que verifica depois da ação? |
| 5 | **Memória** | O que persiste entre sessões? |

Guides e Sensors são os dois lados do [[wiki/concepts/harness-engineering|harness]] (feedforward e feedback). Especificação merece camada própria porque **especificar intenção é o trabalho caro** — gerar código já é quase grátis.

---

## 1. Estrutura (Ambient Affordances)

A organização do repositório é a affordance de maior impacto para agentes ([[wiki/concepts/ambient-affordances]]).

**Três regras:**

1. **Organize por domínio, não por tipo.** Pastas por camada forçam o agente a abrir 7-13 arquivos por feature; em vertical slice seria 1 ([[wiki/concepts/custo-abstracoes-era-ia]]).
2. **Deep modules.** Interface simples escondendo complexidade interna — a IA navega e testa pela interface.
3. **Flat por padrão, abstrai por dor.** Sem ports/adapters/mappers até haver necessidade real ([[wiki/sources/clean-architecture-custando-caro-era-ia]]).

| ✅ Por domínio | ❌ Por tipo |
|----------------|-----------|
| `payments/` (controller + service + repo juntos) | `controllers/` |
| `contracts/` | `services/` |
| `notifications/` | `repositories/` |

**Java + Spring:** `com.empresa.payments` com controller, service e repository no mesmo pacote.
**Python:** `payments/` com `router.py`, `service.py`, `repository.py`.

### Sobre Clean Architecture em enterprise

O erro mais comum não é falta de estrutura — é **over-engineering**: interface por repositório, use case por CRUD, mappers entre 3 camadas de DTO. Cada indireção custa tokens e acurácia.

A regra prática ([[wiki/entities/waldemar-neto|Waldemar Neto]]): DDD estratégico (módulos por domínio) + flat dentro do módulo + abstrai só quando a dor justificar. Os limites vêm de lugares baratos: bounded contexts, tipos fortes, testes de comportamento e lint que impede import entre domínios.

---

## 2. Especificação (Spec + TDD)

### Design Doc como ponto de partida

O ciclo enterprise começa com um **documento de design revisado por humanos** (RFC, ADR ou PRD) — a fonte da verdade auditada ([[wiki/sources/fluxo-completo-dev-avancado-ia]]). A IA avalia o doc, identifica lacunas e dele derivam spec e tasks.

### Spec — linguagem natural estruturada

Spec específica de feature (distinta do contexto geral), operada no ciclo **RPI — Research, Plan, Implement** ([[wiki/sources/spec-driven-guia-completo-waldemar]]): pesquisar em janela dedicada, salvar em markdown, implementar em janela limpa (~30% de 200K tokens).

Ressalva ([[wiki/entities/birgitta-bockeler|Böckeler]], [[wiki/entities/matt-pocock|Matt Pocock]]): spec sozinha é feedforward puro — diz o que fazer, mas não verifica se foi feito certo ([[wiki/concepts/spec-driven-development]]).

### TDD — a especificação executável

O que fecha o loop. Teste como **contrato determinístico** do que "funcionar" significa ([[wiki/concepts/tdd-como-especificacao]]).

```
Humano escreve teste (RED) → Agente implementa (GREEN) → Colaboração refatora (REFACTOR)
```

**Regra de ouro: nunca delegar o RED ao agente.** Quem escreve o teste que falha define o contrato.

O archetype nasce com esqueleto de testes pronto e um slice vertical de exemplo já em TDD.

---

## 3. Guides (Feedforward)

O que o agente lê **antes** de escrever ([[wiki/concepts/harness-engineering]], [[wiki/sources/rules-skills-mcps-subagents-waldemar]]).

| Artefato | Função |
|----------|--------|
| `AGENTS.md` (~200 linhas) | Estrutura do projeto + ponteiros para docs (progressive disclosure) |
| Glossário ubíquo | Alinha termos do domínio (DDD) — funciona como *positive prompt injection* |
| ADRs (`docs/adr/`) | Decisões de design consultáveis |
| Doc de arquitetura | Camadas, fronteiras e regras do bounded context |
| Regras de dados | Schema, validação (Bean Validation / Pydantic) |
| Skills (~66 linhas) | Tática reutilizável: `create-use-case`, `create-test`, "novo agregado" |
| **Config de MCPs** | Contexto externo vivo (ver abaixo) |

### MCPs essenciais

Arquivo de config versionado no repo (`mcp.json`) — o agente já nasce com acesso ao contexto vivo:

- **Board do time** (Atlassian MCP, Azure DevOps MCP) — requisito, critério de aceite, contexto da task.
- **Context7 MCP** — docs correntes das libs/frameworks; antídoto contra alucinação de API.
- **Dados de produção** (opcional, read-only) — decisão de arquitetura informada por dado real.

> **MCP** busca conhecimento que muda e vive em outro lugar. **Skill** é instrução local de como usar. **Doc** é referência persistente. Prefira poucos MCPs sob demanda — excesso estoura a janela ([[wiki/concepts/harness-engineering]]).

---

## 4. Sensors (Feedback)

O que **quebra o build** após a ação. Regra: rode como teste, não como lint ([[wiki/concepts/sensores-computacionais]]).

| Sensor | Java + Spring | Python |
|--------|---------------|--------|
| Type / compile | `javac` + Error Prone | mypy |
| Lint (mensagens custom) | Checkstyle, PMD, SpotBugs | ruff |
| **Fitness de arquitetura** | **[[wiki/entities/archunit|ArchUnit]]** | [[wiki/entities/dependency-cruiser|import-linter]] |
| SAST + secrets | Semgrep + GitLeaks | Semgrep + GitLeaks |
| Quality gate | **SonarQube** | SonarQube |
| Testes unitários | JUnit 5 | pytest |
| Testes E2E | Testcontainers | pytest + testcontainers |
| **[[wiki/concepts/mutation-testing|Mutation testing]]** | **PIT** | mutmut / cosmic-ray |

**[[wiki/entities/archunit|ArchUnit]]** materializa o DDD/Hexagonal como teste — sem ele, a documentação de arquitetura é só feedforward sem feedback.

**SonarQube** é quality gate no CI que **bloqueia o PR** (não só reporta). Agentes dão nova vida ao Sonar porque consomem o output e corrigem issues sozinhos ([[wiki/sources/harness-beyond-skills-sensors]], [[wiki/concepts/sanity-checks]]).

### Gates automatizados

O archetype nasce com gates que rodam sem intervenção, implementando o fluxo que [[wiki/entities/zarathon-viana|Zarathon Viana]] defende ([[wiki/sources/code-review-na-era-dos-agentes]]):

```
Código sobe → CI (gates duros) → IA review (sensor) → Autor corrige → Humano revisa (juiz)
```

**Gate de cobertura:**
- JaCoCo `check` ≥ 80% (Java) / `--cov-fail-under=80` (Python) quebrando o build.
- PIT / mutmut com [[wiki/concepts/mutation-testing|mutation score]] mínimo — evita coverage alta com testes frágeis.
- Hook `agentStop` que dispara testes antes mesmo do commit.

**Gate de segurança:**
- GitLeaks no pre-commit — barra segredos e `.env` que devem estar em variáveis de ambiente (vars/secrets do CI), nunca no código.
- Semgrep + SCA (OWASP Dependency-Check / pip-audit) bloqueantes no CI.
- Security review por IA periódico para concerns semânticos.

> Gates são **sensor**, não juiz. Barram o erro óbvio para o humano focar no erro convincente ([[wiki/concepts/code-review-como-portao]]).

---

## 5. Memória

Preserva decisões entre sessões, sobrevivendo à [[wiki/concepts/compaction-de-contexto|compaction]] ([[wiki/concepts/memoria-longo-prazo-agentes]]).

| Nível | Artefato |
|-------|----------|
| Mínimo | ADRs + `.docs/` com decisões importantes |
| Intermediário | `HANDOFF.md` / state file (o que foi feito, o que falta) |
| Avançado | Daemon MCP de memória + consolidação periódica |

Sem memória, "por que não usamos X aqui?" fica sem resposta no turno 50.

---

## Shift-Left: critérios de review embutidos no template

O que um bom review cobra é previsível. O archetype codifica esses critérios como regra e gate — o agente os satisfaz **antes** de o humano olhar.

### 1. Teste rastreável a requisito

Todo teste aponta para o ADR/spec que satisfaz. Valida a **regra de negócio**, não só "o código roda".

- `@Tag("REQ-014")` no JUnit / `@pytest.mark.req("REQ-014")` no pytest.
- Gate que falha se teste novo não tem vínculo com requisito.

### 2. Branches pequenas e de propósito único

Uma branch = um propósito = um PR revisável (200-400 linhas).

- Convenção de nome: `feat/REQ-014-listagem-pagamentos`.
- Hook `agentStop`/pre-push que barra branches com diff excessivo.
- Conventional Commits via `commit-msg` hook.

### 3. Modelo de geração ≠ modelo de teste/review

Mesmo modelo gerando e validando cai na *homogenisation trap* — erros correlacionados ecoam em vez de se cancelarem.

- Modelo A gera implementação; modelo B gera/avalia testes e faz review.
- Diversificação é também economia ([[wiki/concepts/multimodelo-slm]]).

> O que não se mecaniza — se a abstração escala, se o trade-off cabe, se há alucinação de regra de negócio — continua sendo trabalho humano. O archetype libera a atenção do humano para esses pontos ([[wiki/concepts/automation-complacency|taste e consciência situacional]] como antídoto).

---

## Passos Essenciais

Ordem sugerida (determinístico primeiro, inferencial depois):

1. Bounded contexts + glossário ubíquo
2. Estrutura por domínio + deep modules
3. Config de MCPs versionada (board + Context7)
4. Sensores de arquitetura como teste ([[wiki/entities/archunit|ArchUnit]] / [[wiki/entities/dependency-cruiser|import-linter]])
5. Lint com mensagens custom
6. Esqueleto de testes (unitário + E2E + mutation) com slice vertical em TDD
7. Quality gate do Sonar + gate de cobertura
8. Gate de segurança (GitLeaks + Semgrep + SCA)
9. Regras de shift-left no `AGENTS.md`
10. Hooks de disciplina (`commit-msg`, `agentStop`/pre-push)
11. Template de Spec + skill de RPI
12. CI em ambiente limpo (todos os sensors do zero)
13. `AGENTS.md` + skills
14. ADRs + HANDOFF.md
15. Steering loop — toda falha recorrente vira novo sensor/gate/guide

---

## Checklist de Validação

Use para auditar um archetype existente ou validar um novo. Item sem check = próxima cerca a construir.

### Estrutura
- [ ] Pastas por **domínio** (vertical slice)
- [ ] Módulos **deep** (interface simples, complexidade encapsulada)
- [ ] **Flat por padrão** — sem over-engineering antes da dor
- [ ] Nomenclatura consistente

### Especificação
- [ ] Entrada via **Design Doc / RFC / ADR** revisada por humano
- [ ] Template de **Spec** por feature
- [ ] Slice vertical de exemplo **já em TDD**
- [ ] Regra: **nunca delegar o RED** ao agente

### Guides
- [ ] `AGENTS.md` enxuto (~200 linhas, progressive disclosure)
- [ ] **Glossário ubíquo** (DDD)
- [ ] **ADRs** versionados
- [ ] **Skills** portáveis
- [ ] **Config de MCPs** versionada (board + Context7)

### Sensors (quebram o build)
- [ ] Type/compile + lint com **mensagens custom**
- [ ] **Fitness de arquitetura** bloqueando violação de camada
- [ ] Testes unitários + **E2E**
- [ ] **Mutation testing** com threshold mínimo
- [ ] **Gate de cobertura** quebrando o build
- [ ] **Gate de segurança** bloqueante (Semgrep + GitLeaks + SCA) — chaves e `.env` em vars/secrets, nunca no código
- [ ] **SonarQube** quality gate no CI

### Memória
- [ ] ADRs + `.docs/` com decisões
- [ ] `HANDOFF.md` / state file

### Shift-left e disciplina
- [ ] Teste **rastreável** a requisito/ADR
- [ ] Convenção de **branch por propósito** (`feat/REQ-014-...`)
- [ ] Hook que barra **branches grandes**
- [ ] Conventional Commits via `commit-msg`
- [ ] **Modelo de geração ≠ modelo de teste/review**
- [ ] **Steering loop** ativo

---

## Ver também

- [[wiki/concepts/harness-engineering]] — guides + sensors
- [[wiki/concepts/ambient-affordances]] — estrutura navegável
- [[wiki/concepts/tres-camadas-coding-ia]] — modelo, ferramenta, engenharia
- [[wiki/concepts/tdd-como-especificacao]] — teste como contrato
- [[wiki/concepts/spec-driven-development]] — spec como guide
- [[wiki/concepts/sensores-computacionais]] — camada determinística
- [[wiki/concepts/code-review-como-portao]] — o portão humano
- [[wiki/concepts/mutation-testing]] — detector de testes frágeis
- [[wiki/concepts/property-based-testing]] — complemento ao TDD para invariantes
- [[wiki/concepts/sanity-checks]] — quality gate (SonarQube)
- [[wiki/concepts/automation-complacency]] — o risco de confiar demais
- [[wiki/concepts/custo-abstracoes-era-ia]] — vertical slice > camadas
- [[wiki/concepts/multimodelo-slm]] — diversificação de modelos
- [[wiki/concepts/memoria-longo-prazo-agentes]] — continuidade entre sessões
- [[wiki/entities/archunit]] — fitness de arquitetura (Java)
- [[wiki/entities/dependency-cruiser]] — fitness de arquitetura (JS/TS)
- [[wiki/entities/waldemar-neto]] — Tech Leads Clube
- [[wiki/entities/zarathon-viana]] — As 3 Camadas do Coding com IA
- [[wiki/entities/birgitta-bockeler]] — Harness Engineering / Sensors
- [[wiki/entities/matt-pocock]] — Fundamentos + Deep Modules
- [[wiki/sources/clean-architecture-custando-caro-era-ia]] — flat por padrão, abstrai por dor
- [[wiki/sources/fluxo-completo-dev-avancado-ia]] — setup mínimo e RPI na prática
- [[wiki/sources/spec-driven-guia-completo-waldemar]] — anatomia da spec e state
- [[wiki/sources/code-review-na-era-dos-agentes]] — o fluxo de gates
- [[wiki/essentials/overview-engenharia-na-era-ia]] — síntese geral
