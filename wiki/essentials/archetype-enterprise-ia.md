---
title: "O Essencial ao Construir um Archetype para Projetos Enterprise com IA"
type: synthesis
tags: [archetype, service-template, harness-engineering, ambient-affordances, tdd, spec-driven, java, spring, python]
created: 2026-06-09
updated: 2026-06-09
sources: ["[[wiki/sources/arquitetura-na-era-dos-agentes]]", "[[wiki/sources/maintainability-sensors]]", "[[wiki/sources/harness-engineering-fowler]]", "[[wiki/sources/tdd-na-era-dos-agentes]]", "[[wiki/sources/spec-driven-development]]", "[[wiki/sources/spec-driven-guia-completo-waldemar]]", "[[wiki/sources/code-review-na-era-dos-agentes]]", "[[wiki/sources/clean-architecture-custando-caro-era-ia]]", "[[wiki/sources/fluxo-completo-dev-avancado-ia]]", "[[wiki/sources/rules-skills-mcps-subagents-waldemar]]", "[[wiki/sources/software-fundamentals-matter-more-than-ever]]"]
---

# O Essencial ao Construir um Archetype para Projetos Enterprise com IA

Um *archetype* (service template) para projetos comerciais de grande porte não é só "código que compila". Na era dos agentes, é um repositório com as **cercas já montadas** — o ambiente onde o agente começa a trabalhar dentro de fronteiras determinísticas em vez de um campo aberto.

> Times greenfield podem embutir *harnessability* desde o dia 1. As escolhas de tecnologia e arquitetura determinam o quão governável o código vai ser. — [[wiki/concepts/ambient-affordances]]

Este artigo descreve a anatomia desse template e os passos para construí-lo, com exemplos em **Java + Spring** e **Python**.

---

## As 5 Camadas de um Archetype AI-Ready

Um archetype governável é a soma de cinco camadas. Cada uma responde a uma pergunta diferente sobre o trabalho do agente:

```
1. Estrutura      → define POR ONDE o agente anda     (ambient affordances)
2. Especificação  → define O QUE ele deve produzir     (Spec + TDD)
3. Guides         → direcionam ANTES da ação           (feedforward)
4. Sensors        → verificam DEPOIS da ação           (feedback)
5. Memória        → preservam decisão ENTRE sessões    (continuidade)
```

As camadas 3 e 4 são os dois lados do [[wiki/concepts/harness-engineering|harness]] (feedforward/feedback). A camada 2 merece destaque próprio porque, na era dos agentes, **especificar intenção é o trabalho caro** — gerar código já é quase grátis.

---

## Camada 1 — Estrutura (Ambient Affordances)

Define **por onde** o agente pode andar. É a affordance de maior impacto ([[wiki/concepts/ambient-affordances]]).

- **Organize por domínio, não por camada.** O *Navigation Paradox* mediu que pastas por camada forçam o agente a abrir 7-13 arquivos por feature; em vertical slice seria 1 ([[wiki/concepts/custo-abstracoes-era-ia]]).
- **Deep modules** — interface simples escondendo complexidade interna; a IA navega e testa pela interface.
- **Nomenclatura consistente** + CI pré-configurado.

| Por domínio ✅ | Por tipo ❌ |
|---------------|-----------|
| `payments/` (controller + service + repository juntos) | `controllers/` |
| `contracts/` | `services/` |
| `notifications/` | `repositories/` |

**Java + Spring:** pacote `com.empresa.payments` com `PaymentController`, `PaymentService`, `PaymentRepository` no mesmo bounded context — não `controllers/`, `services/`, `repositories/` horizontais.

**Python:** pacote `payments/` com `router.py`, `service.py`, `repository.py` — slice vertical por domínio.

### Estratégico primeiro, flat depois, abstrai por dor

Num archetype enterprise, o erro mais comum é o oposto do caos: **over-engineering** de Clean Architecture (interface por repositório, use case por CRUD, três camadas de mappers). Cada abstração sem propósito custa tokens, indireção e acurácia da IA ([[wiki/sources/clean-architecture-custando-caro-era-ia]]). A regra do Waldemar:

1. **DDD estratégico** — módulos por domínio (billing, orders, identity), cada um independente. Barato e de alto impacto.
2. **Flat dentro do módulo** — entrada/saída + lógica + persistência; sem ports/adapters/mappers até a dor justificar.
3. **Abstrai só por dor real** — trocou a dependência nos últimos 2 anos? Tem 2º uso real? Senão, não abstrai.

> "Se a IA gera 10x mais rápido, ausência de estrutura vira caos 10x mais rápido." — verdade, mas os limites vêm de lugares **baratos**: bounded contexts, tipos fortes nos contratos entre módulos, testes de comportamento e lint que impede import entre domínios. Esses são os mesmos sensores das camadas seguintes, não cerimônia tática.

---

## Camada 2 — Especificação (Spec + TDD)

Define **o que** o agente deve produzir. Tem duas formas complementares: uma em linguagem natural (Spec) e uma executável e determinística (TDD).

### A entrada: Design Doc / RFC / ADR revisado por humano

Antes da spec, o ponto de partida enterprise é um **documento de design revisado por humanos** (RFC, ADR ou PRD) — a fonte da verdade escrita e auditada ([[wiki/sources/fluxo-completo-dev-avancado-ia]]). Times que já escrevem RFCs/ADRs partem na frente: a IA avalia o doc, identifica lacunas antes de codar, e dele derivam spec e tasks. É o que ancora a regra de *teste rastreável a requisito* (shift-left).

### Spec — feedforward em linguagem natural

A spec é um guide específico de feature, distinto do *memory bank* (contexto geral) ([[wiki/concepts/spec-driven-development]]). Vale o princípio **spec-first** (pensar e estruturar antes de pedir), mas com a ressalva crítica de Böckeler e Matt Pocock: spec sozinha é **feedforward puro** — diz o que fazer, não verifica se foi feito certo, e o agente frequentemente ignora partes dela.

O archetype pode shippar a skill de spec e operar o ciclo **RPI — Research, Plan, Implement** ([[wiki/sources/spec-driven-guia-completo-waldemar]]): pesquisar numa janela dedicada, salvar spec/design/tasks em markdown, e implementar numa janela limpa. Isso mantém a janela de contexto baixa (~30% de 200K) e escala features grandes sem alucinação.

### TDD — a especificação executável

Por isso a espinha dorsal da camada 2 é o [[wiki/concepts/tdd-como-especificacao|TDD]]: na era dos agentes, teste não é safety net, é **contrato determinístico** do que "funcionar" significa.

```
Humano escreve teste (RED) → Agente implementa (GREEN) → Colaboração refatora (REFACTOR)
```

**Regra de ouro: nunca delegar o RED ao agente.** Quem escreve o teste que falha define o contrato. Teste escrito depois do código é "espelho autorreferente" — confirma os próprios bugs (coverage de 92% com mutation score de 4%).

O archetype deve nascer com o esqueleto de teste pronto e um exemplo de slice vertical já testado, demonstrando o ciclo. TDD é o que **fecha o loop** que a spec deixa aberto.

---

## Camada 3 — Guides (Feedforward)

O que o agente lê **antes** de escrever. São os guides do harness ([[wiki/concepts/harness-engineering]], [[wiki/sources/rules-skills-mcps-subagents-waldemar]]).

| Peça | Papel | Java + Spring | Python |
|------|-------|---------------|--------|
| `AGENTS.md` no root | Estrutura + ponteiros, máx ~200 linhas | idem | idem |
| Glossário ubíquo (DDD) | Alinha termos do domínio | `glossary.md` por contexto | idem |
| ADRs | Decisões de design consultáveis | `docs/adr/` | `docs/adr/` |
| Doc de arquitetura | Hexagonal/DDD, camadas e fronteiras | overview + diagrama | overview + diagrama |
| Regras de estrutura de dados | Schema, contratos, validação | Bean Validation + skill "novo agregado" | Pydantic + skill |
| Skills (~66 linhas, portáveis) | Tática local reutilizável | `create-use-case`, `create-controller`, `create-test` | `create-endpoint`, `create-repository`, `create-test` |
| **MCPs** (config no repo) | Contexto externo dinâmico (API para LLMs) | mesma config | mesma config |

As mensagens importam: glossário e regras de dados funcionam como *positive prompt injection*. Use **progressive disclosure** — `AGENTS.md` enxuto apontando para docs sob demanda, não tudo carregado de início.

### O arquivo de config de MCPs

O archetype deve trazer um arquivo de config de MCPs versionado (ex: `mcp.json`/`.mcp.json` no repo), para o agente já nascer com acesso ao **contexto vivo** do negócio e da tecnologia — não chumbado em prompt ([[wiki/sources/rules-skills-mcps-subagents-waldemar]], [[wiki/sources/fluxo-completo-dev-avancado-ia]]).

MCPs essenciais para um archetype:

- **Gestão / dashboards:** Atlassian MCP (Jira, Confluence), Azure DevOps MCP, ou o board que o time usa. Traz o requisito, o critério de aceite e o contexto da task para dentro da sessão — o que alimenta diretamente a regra de *teste rastreável a requisito* (shift-left).
- **Documentação atualizada:** **Context7 MCP** — docs correntes das libs/frameworks, antídoto contra alucinação de API (método que não existe, versão errada).
- **Dados de produção (opcional, read-only):** decisão de arquitetura informada por dado real, não chutada.

> Distinção-chave ([[wiki/concepts/harness-engineering]]): **MCP** busca conhecimento que muda e vive **em outro lugar** (Jira, docs). **Skill** é a instrução local de como usar. **Doc** é a referência persistente do projeto. Cuidado com excesso: dezenas de MCPs carregados estouram a janela — prefira poucos, sob demanda (regra dos ~40%).

---

## Camada 4 — Sensors (Feedback)

O que **quebra o build** depois da ação ([[wiki/concepts/sensores-computacionais]], [[wiki/sources/maintainability-sensors]]). Regra transversal: **rode como teste (quebra build), não como lint (só avisa)**.

| Sensor | Java + Spring | Python | Observação |
|--------|---------------|--------|------------|
| Compile / type | `javac` + Error Prone | mypy | base determinística |
| Lint com mensagem custom | Checkstyle, PMD, SpotBugs | ruff | complexidade, tamanho de função/arquivo, max args — não vêm no preset padrão |
| **Fitness de arquitetura** | **ArchUnit** | import-linter | quebra build em violação de camada — materializa o DDD/Hexagonal documentado |
| SAST + secrets | Semgrep + GitLeaks (pre-commit) | Semgrep + GitLeaks | |
| Qualidade contínua | **SonarQube** / SonarLint | SonarQube | quality gate no CI; evolução do Sonar (sanity checks) |
| Testes unitários | JUnit 5 | pytest | |
| Testes E2E / acceptance | Spring Boot Test + Testcontainers | pytest + testcontainers | a IA gera bem |
| **Mutation testing** | **PIT (pitest)** | mutmut / cosmic-ray | crucial quando a IA escreve os testes — coverage alta ≠ teste efetivo |

O **ArchUnit** é o coração desta camada em Java: sem ele, o DDD/Hexagonal da camada 3 é só feedforward sem feedback. Cross-file concerns (modularidade, acoplamento) precisam de **sensor inferencial** (review por IA) periódico, pois métricas puras geram ruído.

O **SonarQube** entra como *quality gate* no CI — a evolução natural do "cheque de sanidade" da era pré-IA ([[wiki/concepts/sanity-checks]]). A virada é que organizações já tinham SonarQube "juntando poeira"; o agente dá nova vida a ele porque consome o output e corrige os issues sozinho ([[wiki/sources/harness-beyond-skills-sensors]]). No archetype, configure o quality gate para **quebrar o PR** (não só reportar) em bugs, vulnerabilidades e code smells acima do limite.

### Os Gates Automatizados (Hooks e Workflows)

Sensores só valem se **rodam sozinhos**. O archetype deve nascer com os gates automatizados — em pre-commit hooks (rápido, local) e em CI workflows (completo, ambiente limpo) — implementando o fluxo que [[wiki/entities/zarathon-viana|Zarathon]] defende em [[wiki/sources/code-review-na-era-dos-agentes]]:

```
Código sobe → CI (gates duros) → IA review (sensor) → Autor corrige → Humano revisa (juiz)
```

Dois gates são obrigatórios num archetype AI-ready, porque endereçam exatamente onde o agente erra "com cara de certo":

**1. Gate de cobertura mínima de testes.**
Sempre que código é gerado, o build falha se a cobertura cair abaixo de um piso. Isso ataca o "teatro de coverage" e força o ciclo TDD da camada 2. Combine com mutation testing para não cair na armadilha de coverage alta com testes frágeis ([[wiki/concepts/mutation-testing]]).

- **Java + Spring:** JaCoCo com `check` rule (ex: `LINE` ≥ 80%) quebrando o `mvn verify`; PIT com threshold de mutation score mínimo.
- **Python:** `pytest --cov --cov-fail-under=80`; mutmut no gate periódico.
- **Hook/Workflow:** rodar no CI a cada PR e, idealmente, um hook `postToolUse`/`agentStop` que dispara os testes assim que o agente termina de gerar código — feedback antes mesmo do commit.

**2. Gate de segurança da empresa.**
Sempre que um código é gerado, validar contra as regras de segurança da organização *antes* de chegar ao humano. O agente alucina libs, vaza segredos e ignora padrões de input validation — esse gate é a cerca determinística contra isso.

- **Determinístico (computacional):** Semgrep com o ruleset da empresa, GitLeaks no pre-commit, SCA de dependências (Java: OWASP Dependency-Check; Python: pip-audit), SAST.
- **Inferencial (IA):** *security review* periódico por agente, para concerns semânticos que o Semgrep não pega ([[wiki/sources/maintainability-sensors]]).
- **Hook/Workflow:** GitLeaks como pre-commit (barra o segredo antes do commit) + Semgrep/SCA como workflow de CI bloqueante no PR.

> Princípio: o gate é **sensor**, não juiz. Ele barra o erro óbvio e o padrão conhecido para que o humano gaste energia no erro convincente — lógica de negócio plausível mas errada, acoplamento que quebra o sistema ([[wiki/concepts/code-review-como-portao]]).

---

## Camada 5 — Memória

Preserva decisão **entre sessões**, sobrevivendo à [[wiki/concepts/compaction-de-contexto|compaction]] ([[wiki/concepts/memoria-longo-prazo-agentes]]).

- **Mínimo:** ADRs + `.docs/` no root com decisões importantes.
- **Intermediário:** `HANDOFF.md` / progress file com estado atual da implementação — o que foi feito, o que deu errado, o que falta.
- **Avançado:** daemon MCP de memória + consolidação periódica.

Sem esta camada, "por que decidimos não usar X aqui?" vira pergunta sem resposta no turno 50.

---

## Shift-Left: o que sabemos que será cobrado já vira regra

Sabemos de antemão o que um bom review exige. Então, em vez de esperar o portão humano apontar, o archetype **codifica esses critérios como regra (feedforward) e gate (feedback)** — o agente os satisfaz antes de o humano olhar. Cada item abaixo é um critério de review transformado em parte do template.

### 1. Teste rastreável a ADR / Spec — e validando regra de negócio

Todo teste deve apontar para o requisito que satisfaz. No formato de spec (`requirements.md`, `design.md`, `tasks.md`) ou no ADR correspondente, o teste deixa de validar só "o código roda" e passa a validar a **regra de negócio acordada**. É o antídoto contra o erro mais caro: lógica plausível, bem escrita e errada.

- **Regra no `AGENTS.md`:** "todo teste referencia o requisito/ADR que cobre (ex: `// REQ-014` ou tag/`@Tag`); comportamento sem requisito não entra."
- **Java + Spring:** `@Tag("REQ-014")` no JUnit + naming `should<Comportamento>_when<Condição>` derivado do critério de aceite.
- **Python:** marcador `@pytest.mark.req("REQ-014")` + docstring citando o critério.
- **Gate:** check que falha se um teste novo não tem vínculo com requisito/ADR; conecta com a regra de ouro do TDD — o humano escreve o RED a partir do critério de aceite, não o agente.

### 2. Branches pequenas e de propósito único (via hook/workflow)

A eficácia da revisão desaba depois de 200-400 linhas (detecção ~87% em PRs < 100 linhas, ~28% acima de 1000). O archetype não deixa isso para a boa vontade do agente: automatiza o limite — uma branch resolve **um único propósito** e vira um PR pequeno e revisável.

- **Regra no `AGENTS.md`:** "uma branch por propósito; gere em fatias verticais pequenas; não acumule mudanças não relacionadas na mesma branch."
- **Convenção de branch:** nome derivado do requisito/task (ex: `feat/REQ-014-listagem-pagamentos`), reforçando a rastreabilidade do item 1.
- **Hook/Workflow:** hook `agentStop`/pre-push que avisa (ou bloqueia) branches com diff acima de um teto de linhas/arquivos; workflow de CI que sinaliza PR grande demais para review confiável.
- **Conventional Commits** validados por hook `commit-msg` — histórico legível e changelog/rollback automáticos para volume industrial de mudanças.

### 3. Modelo de geração ≠ modelo de teste/review

Mesmo modelo gerando código e validando cai na *homogenisation trap*: erros correlacionados ecoam em vez de se cancelarem. O archetype define, por config, modelos distintos para cada papel.

- **Regra/config:** modelo A gera implementação; modelo B (diferente) gera/avalia testes e faz a primeira passada de review. Diversificação também é economia ([[wiki/concepts/multimodelo-slm]]).
- **Princípio:** a IA que revisa é **sensor**, nunca juiz — e nunca o mesmo "juiz" que escreveu o código.

> O que não dá para mecanizar — se a abstração vai escalar, se o trade-off cabe na arquitetura, se há alucinação de regra de negócio disfarçada — continua sendo trabalho do humano. O archetype existe para **liberar a atenção humana para esses pontos**, automatizando todo o resto. Cada novo padrão de erro recorrente vira mais uma regra aqui (steering loop).

---

## Passos Essenciais (ordem sugerida)

A sequência segue o gradiente da wiki: determinístico forte primeiro, inferencial depois.

1. **Bounded contexts + glossário ubíquo** — antes de qualquer pasta. Feedforward de maior alavanca.
2. **Estrutura por domínio + deep modules** — vertical slices, não camadas horizontais.
3. **Config de MCPs versionada** — Atlassian/Azure (board) + Context7 (docs) no `mcp.json` do repo.
4. **Sensores de arquitetura como teste** — ArchUnit (Java) / import-linter (Python) quebrando o build.
5. **Lint com mensagens custom** — complexidade, tamanho, max args; mensagens que orientam autocorreção.
6. **Esqueleto de testes nas 3 camadas** — unitário, E2E (Testcontainers) e mutation (PIT/mutmut) rodando no CI, com um slice vertical de exemplo já em TDD.
7. **Quality gate do SonarQube + gate de cobertura** — JaCoCo/`--cov-fail-under` + threshold de mutation score; Sonar bloqueando o PR.
8. **Gate de segurança** — GitLeaks no pre-commit, Semgrep + SCA bloqueantes no CI, security review por IA periódico.
9. **Regras de shift-left no `AGENTS.md`** — teste rastreável a requisito/ADR, branch pequena de propósito único, modelo de geração ≠ modelo de teste/review.
10. **Hooks de disciplina** — `commit-msg` (Conventional Commits) e `agentStop`/pre-push que barra branches com diff grande demais.
11. **Template de Spec** — estrutura de spec por feature + a regra de nunca delegar o RED.
12. **CI em ambiente limpo** — todos os sensores e gates repetidos do zero.
13. **`AGENTS.md` + skills** — `create-use-case`, `create-test`, e a skill de "novo agregado" que aplica as regras de dados.
14. **ADRs + HANDOFF.md** — memória entre sessões.
15. **Steering loop** — toda falha recorrente do agente vira um novo sensor, gate ou guide. O archetype evolui.

---

## Síntese em uma frase

> Um archetype AI-ready embute as cinco camadas — estrutura, especificação, guides, sensors e memória — para que o agente comece dentro do harness, não num campo aberto. Greenfield é a única chance de fazer isso de graça.

---

## Checklist: o archetype tem a estrutura ideal?

Use para auditar um archetype existente ou validar um novo. Se um item não puder ser marcado, ali está a próxima cerca a construir.

### Camada 1 — Estrutura
- [ ] Pastas organizadas **por domínio** (vertical slice), não por tipo/camada
- [ ] Módulos **deep** (interface simples escondendo complexidade)
- [ ] Nomenclatura consistente e CI pré-configurado
- [ ] Estrutura **flat por padrão** — sem ports/adapters/mappers antes da dor justificar

### Camada 2 — Especificação
- [ ] Existe entrada de **Design Doc / RFC / ADR** revisada por humano
- [ ] Template de **Spec** por feature no repo
- [ ] Esqueleto de testes com um **slice vertical de exemplo já em TDD**
- [ ] Regra explícita: **nunca delegar o RED** ao agente

### Camada 3 — Guides
- [ ] `AGENTS.md` enxuto (~200 linhas) com estrutura + ponteiros (progressive disclosure)
- [ ] **Glossário ubíquo** (DDD) no repo
- [ ] **ADRs** versionados
- [ ] Skills portáveis (`create-use-case`, `create-test`, "novo agregado")
- [ ] **Config de MCPs** versionada (Atlassian/Azure + Context7)

### Camada 4 — Sensors (quebram o build, não só avisam)
- [ ] Type/compile + lint com **mensagens custom**
- [ ] **Fitness de arquitetura** (ArchUnit / import-linter) bloqueando violação de camada
- [ ] Testes unitários + **E2E** (Testcontainers)
- [ ] **Mutation testing** (PIT / mutmut) com threshold mínimo
- [ ] **Gate de cobertura** mínima quebrando o build
- [ ] **Gate de segurança** (Semgrep + GitLeaks + SCA) bloqueante
- [ ] **Quality gate do SonarQube** no CI

### Camada 5 — Memória
- [ ] ADRs + `.docs/` no root com decisões importantes
- [ ] `HANDOFF.md` / state file para continuidade entre sessões

### Shift-left e disciplina
- [ ] Teste **rastreável** a requisito/ADR (tag/marcador)
- [ ] Hook que barra **branches grandes** (pre-push/`agentStop`); Conventional Commits via `commit-msg`
- [ ] Convenção de **branch por propósito** ligada ao requisito (ex: `feat/REQ-014-...`)
- [ ] Config separando **modelo de geração ≠ modelo de teste/review**
- [ ] **Steering loop** ativo: toda falha recorrente vira novo sensor/gate/guide

---

## Ver também

- [[wiki/concepts/harness-engineering]] — guides (feedforward) + sensors (feedback)
- [[wiki/concepts/ambient-affordances]] — estrutura navegável e service templates
- [[wiki/concepts/tdd-como-especificacao]] — teste como contrato executável
- [[wiki/concepts/spec-driven-development]] — spec como guide (com limites)
- [[wiki/concepts/sensores-computacionais]] — a camada determinística
- [[wiki/concepts/code-review-como-portao]] — o portão humano e o fluxo de gates
- [[wiki/concepts/mutation-testing]] — detector de testes frágeis no gate de cobertura
- [[wiki/concepts/sanity-checks]] — quality gate (SonarQube) como cheque de sanidade
- [[wiki/concepts/custo-abstracoes-era-ia]] — por que vertical slice > camadas para agentes
- [[wiki/concepts/memoria-longo-prazo-agentes]] — continuidade entre sessões
- [[wiki/sources/clean-architecture-custando-caro-era-ia]] — estratégico primeiro, flat depois, abstrai por dor
- [[wiki/sources/fluxo-completo-dev-avancado-ia]] — setup mínimo do repo, design doc como entrada, RPI na prática
- [[wiki/sources/spec-driven-guia-completo-waldemar]] — RPI, anatomia da spec e arquivo de state
- [[wiki/essentials/overview-engenharia-na-era-ia]] — a síntese geral
