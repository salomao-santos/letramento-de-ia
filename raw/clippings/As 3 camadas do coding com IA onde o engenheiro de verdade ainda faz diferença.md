---
title: "As 3 camadas do coding com IA: onde o engenheiro de verdade ainda faz diferença"
source: "https://zaratips.substack.com/p/as-3-camadas-do-coding-com-ia-onde"
author:
  - "[[Zarathon \"Zara\" Viana]]"
published: 2026-04-21
created: 2026-06-08
description: "Harness Engineering virou moda. Mas tem um detalhe que ninguém tá contando: a camada onde você mais tem controle é justamente a que todo mundo tá ignorando."
tags:
  - "clippings"
---
Augusto, sênior há oito anos, abriu o Cursor pela primeira vez convencido de que ia virar o jogo. Pegou uma tarefa de duas horas, ligou o Claude 3.7 Sonnet, começou a promptar.

Quatro horas depois, ainda tava lá. Código funcionando, mas feio pra caralho. Testes? Nem lembrou. Linter? O que o agente gerou passou raspando. Ele fechou o notebook e pensou: *“caramba, ficou rápido!”*.

Ficou nada. Ficou 19% mais lento.

Não é história. É o resultado de um experimento controlado do METR com desenvolvedores seniores trabalhando em repositórios open source que eles mesmos mantêm.¹ Os caras acharam que a IA tinha acelerado eles em 20%. Na realidade, atrasou em 19%. Uma diferença de 43 pontos percentuais entre o que eles sentiam e o que de fato aconteceu.

E a pergunta que fica é: **por que isso acontece?**

A resposta tá numa coisa que o Martin Fowler, a Birgitta Böckeler (Thoughtworks), a galera do OpenAI e o Henrique Bastos vêm chamando de *Harness Engineering*. Mas eu quero ir além da definição que tá circulando. Porque, pragmaticamente, o engenheiro brasileiro que tá sentado no Cursor hoje de manhã precisa entender o jogo em três camadas. Não duas.

Vou explicar, tenha nervo.

![](https://substackcdn.com/image/fetch/$s_!q9zh!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5bdd3534-601b-43ca-bdef-9d305790908a_2752x1536.png)

## O que é Harness Engineering, pra gente começar do começo

“Harness” vem de arreio de cavalo. Rédea, sela, freio, bridão. O modelo é o cavalo, potente, rápido, mas sem rumo. O *harness* é tudo que canaliza essa potência numa direção útil.

A literatura atual define assim: o termo harness virou atalho pra tudo que está em um agente de IA exceto o modelo em si. Agent = Model + Harness. Essa é a definição do Fowler, abraçada pelo OpenAI, LangChain, Anthropic e pela turma da Thoughtworks.

Aí vem a provocação prática: tá, mas o engenheiro comum, aquele que tá no dia a dia escrevendo código no QuintoAndar, no iFood, no Nubank, onde ele tem controle real? Porque se Harness Engineering vira só um debate de quem escolhe tool e faz context engineering, a gente perdeu o ponto.

Por isso eu gosto de pensar em três camadas, não duas. E a sacada central que eu quero deixar aqui é simples:

> **Quanto mais próximo do modelo, menos controle você tem. Quanto mais próximo da engenharia de software clássica, mais controle você tem.**

Vou abrir uma por uma.

![](https://substackcdn.com/image/fetch/$s_!TO17!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9382dfec-e11d-4d92-a283-fe7781837bf2_1606x1266.png)

## Camada 1. O modelo: o cavalo que você escolhe, mas não doma

Essa é a base. E aqui, seja honesto: você não controla porra nenhuma.

Você não treina o modelo. Você não ajusta peso. Você não muda função de custo. Você **escolhe**. E a escolha tem peso, um peso gigantesco no resultado final.

### A literatura tá dizendo que “só o harness importa”. Eu discordo.

Tem gente falando que a LangChain provou definitivamente que o modelo importa menos do que o sistema ao redor. O agente de coding deles pulou de 52,8% pra 66,5% no Terminal Bench 2.0, do Top 30 pro Top 5, sem mudar nada no modelo. Só mudaram o harness.

Ok. Verdade. Mas isso não quer dizer que modelo não importa. Quer dizer que, dado um modelo capaz, o harness faz a diferença entre flop e sucesso. Se você pegar um modelo ruim, nenhum harness do mundo salva.

### As diferenças reais entre modelos (pra você não achar que é tudo igual)

Cada modelo tem personalidade. E essa personalidade determina o que você vai conseguir fazer no dia a dia.

**Claude Sonnet / Opus (Anthropic)**: historicamente fortes em coding task e long-running agents. O Claude Code é um caso específico onde modelos de coding de fronteira são pós-treinados nos seus harnesses (ex: Claude em Claude Code, GPT-5 Codex em Codex). Ou seja, o modelo foi treinado sabendo que ia rodar naquele harness. Isso é vantagem competitiva.

**GPT-5 / Codex (OpenAI)**: o Codex é tão acoplado ao seu harness que o OpenCode, construído como alternativa open-source ao Claude Code, teve que adicionar uma ferramenta apply\_patch especificamente pra modelos GPT/Codex, imitando o harness do Codex pra melhorar a performance.

**Gemini (Google)**: janela de contexto gigante, bom pra análise de codebase grande, mas historicamente menos “agressivo” em mudanças autônomas.

**Modelos open-source (Qwen, DeepSeek, Llama)**: custo zero, mas você paga em qualidade e em trabalho de harness. Vira o jogo pra quem tem compliance pesado ou trabalha com dado sensível.

### ⚠️ Alerta que quase ninguém tá dando: o preço que você paga hoje é mentira

Antes de seguir, precisa parar aqui e falar de uma coisa que vai mudar essa camada nos próximos dois anos: **os modelos que você usa hoje estão sendo subsidiados**. Pesadamente.

O preço que tu paga na API da OpenAI, da Anthropic, do Claude Pro, do ChatGPT Plus, não cobre o custo real de servir aquele token. Quem tá pagando a diferença é investidor. E investidor não paga conta pra sempre.

Alguns números pra dar a dimensão:

A OpenAI gastou aproximadamente 8,67 bilhões de dólares em inferência nos primeiros nove meses de 2025, quase o dobro do que arrecadou no mesmo período. Sam Altman admitiu publicamente que eles perdem dinheiro até na assinatura ChatGPT Pro de 200 dólares por mês.²

A Anthropic, segundo filing legal do CFO Krishna Rao em março de 2026, arrecadou “mais de 5 bilhões” e gastou “mais de 10 bilhões” em inferência e treinamento. Em 2024 a margem bruta da empresa foi negativa em 94%.³

O Dario Amodei, CEO da Anthropic, falou no DealBook Summit de dezembro que “existem alguns players que estão jogando YOLO, e eu tô muito preocupado”. Ele não tava falando de ceticismo com IA. Tava falando de risco de timing, empresas apostando certo na IA mas errado em quando a economia vai fechar.

O Google subsidia o Gemini com receita de publicidade do Search. O dia que o Search cair, cai junto. A Microsoft tá jogando 13 bilhões na OpenAI e o SoftBank comprometeu mais 41 bilhões. Nada disso é lucro. Tudo isso é tapar buraco.

**O que isso significa pra você, engenheiro brasileiro fazendo coding com IA hoje?**

Significa que saber escolher modelo não vai ser só uma decisão técnica. Vai ser uma decisão econômica, e em breve. Os sinais já tão aparecendo: limites de uso apertando (quem usa Claude Code já sentiu), planos sendo reestruturados, features indo pro tier enterprise, rate limits mais agressivos.

Quando o subsídio acabar, as opções dos labs são poucas: subir preço (provavelmente 2x a 5x o que você paga hoje), apertar limite, ou botar propaganda dentro do produto. Provavelmente um mix dos três.

Quem trabalha hoje só dominando uma ferramenta com um modelo específico vai ter um choque de realidade quando a conta chegar no time financeiro. Um time que custa 5 mil dólares por mês em API pode virar 20 mil quando o preço normalizar.

Por isso a gente volta pra sacada central do artigo: **não trave seu workflow num único modelo ou ferramenta**. Arquitete pra ser agnóstico. Invista no que é seu, na camada 3, que é onde o custo não explode quando a Anthropic ou a OpenAI resolverem fechar a conta.

Essa camada 1 vai virar commodity? Talvez. Vai virar cara? Com certeza em algum momento. Quem tá preparando só hoje e não os próximos 24 meses vai pagar o pato.

### O ponto prático

Você não controla o modelo, mas **controla a escolha**. E essa escolha casca no bolso, na latência e na qualidade, agora e no futuro. Um time que escolhe Claude Opus 4.5 vai ter resultado diferente de um time no GPT-4o-mini. O co-CEO do Spotify Gustav Soderstrom afirmou na earnings call do Q4 2025 que engenheiros sêniores migraram inteiramente de escrever sintaxe pra gerar e supervisionar código de IA desde dezembro de 2025, apoiados em duas tecnologias específicas: Claude Code com Opus 4.5, e um sistema interno do Spotify chamado Honk.

Escolha errada aqui e as outras duas camadas ficam remando contra a maré.

Mas, e aqui é importante, escolha certa aqui **não garante** resultado. É condição necessária, não suficiente.

## Camada 2. A ferramenta: onde você começa a ter as rédeas

Aqui é onde mora Claude Code, Cursor, Codex, Windsurf, Cline, Aider, GitHub Copilot. E é onde entra de fato o *Harness Engineering* na definição da literatura.

O seu controle aqui aumenta, mas ainda é parcial. Você não escreve a ferramenta. Você **configura** e **estende**.

### O que a ferramenta faz por você (e o que ela não faz)

Cada ferramenta traz um harness embutido. O Fowler é direto sobre isso: em agentes de coding, parte do harness já vem pronta (via system prompt, mecanismo de retrieval escolhido, ou mesmo sistema sofisticado de orquestração). Mas agentes de coding também fornecem aos usuários muitas features pra construir um harness externo específico pro caso de uso e sistema deles.

Traduzindo em português claro: tem o harness que vem de fábrica, e tem o harness que você constrói por cima.

### As diferenças reais entre ferramentas

**Claude Code**: orientado a terminal, agentic-first, forte em long-running tasks, suporta sub-agents e skills. Tu escreve um `CLAUDE.md` no root do projeto e ele carrega como contexto permanente.

**Cursor**: inline, editor-first, forte em autocomplete e chat contextual. Config via `.cursorrules`. Histórico de uso marcado pelo estudo do METR. Desenvolvedores tipicamente usavam o Cursor por apenas algumas dezenas de horas antes e durante o estudo. Ou seja, pouca proficiência quer dizer pouco resultado.

**GitHub Copilot**: autocomplete-first, menos agentic, mais discreto. Integrado ao ecossistema GitHub.

**Codex (OpenAI)**: agent-first, roda em ambiente isolado, bom pra task-oriented work. O próprio OpenAI construiu em cima dele uma aplicação de produção com mais de 1 milhão de linhas de código sem uma única linha escrita por mãos humanas.

**OpenCode**: aqui mora uma peça importante que muita gente ignora. É um agente de coding open source que roda no terminal, com mais de 140 mil estrelas no GitHub e mais de 6,5 milhões de devs usando mensalmente (segundo a própria página oficial do projeto). A filosofia é clara: ser agnóstico de provider. Anthropic, OpenAI, Google, Bedrock, Groq, Azure, OpenRouter, ou modelo local auto-hospedado, tu pluga o que quiser. Isso é importante no contexto do alerta econômico que eu fiz lá em cima: num mundo onde os preços dos modelos vão subir, ter uma ferramenta que não te prende a um provider é hedge. Mudou o jogo na Anthropic? Troca pro Gemini. Ficou caro demais? Joga num Qwen self-hosted. OpenCode dá essa flexibilidade. Ponto negativo: exige mais configuração e menos “mágica pronta” que Claude Code.

**Pi**: o oposto filosófico de quase todas as outras. É um harness minimalista escrito pelo Mario Zechner. Quatro ferramentas built-in só: read, write, edit e bash. System prompt de aproximadamente 300 palavras, um dos mais enxutos do mercado. Sem MCP, sem sub-agents, sem plan mode, sem permission popups, sem to-do integrado. O lema do projeto é literal: “adapte o Pi ao seu workflow, não o contrário”. Tudo é extensão que tu escreve ou instala. A proposta é tratar a janela de contexto como recurso escasso e não desperdiçar token com feature que tu não vai usar. É ferramenta pra quem quer controle fino e entende o que tá fazendo. Se tu gosta de configurar, o Pi vai te dar liberdade que Claude Code não dá. Se tu quer ligar e sair usando, vai achar o Pi seco demais.

**Windsurf, Cline, Aider**: outras alternativas open ou semi-open, cada uma com filosofia diferente.

### O que você controla nessa camada

Contexto persistente: AGENTS.md, CLAUDE.md,.cursorrules. O Fowler chama isso de “guides”, instruções feedforward que canalizam o comportamento do agente.

Tools e MCPs: quais ferramentas o agente pode chamar, quais permissões ele tem.

Sub-agents: divisão de tarefas em contextos isolados, pra não poluir o contexto principal.

Hooks: scripts que rodam antes ou depois de uma ação do agente.

Skills: módulos de conhecimento que o agente ativa sob demanda.

Tudo isso é extensibilidade da ferramenta. Você mexe nos knobs, mas não constrói o motor.

### O perigo dessa camada

É aqui que a galera se perde. Passam semanas tunando `.cursorrules`, MCPs, sub-agents. Criam um harness pomposo por fora da ferramenta, acreditando que tão fazendo *a* engenharia da era IA.

E tão. Só que parcialmente. Porque tem uma camada abaixo que pesa mais. Muito mais.

## Camada 3. A engenharia de software: onde o bom engenheiro se destaca

Agora a gente chega onde a terra tá firme. Onde você tem controle quase total. Onde o engenheiro de verdade ainda faz diferença.

Essa é a camada das boas práticas de engenharia. Velhas, conhecidas, meio esquecidas por muita gente. E que voltam com força total agora porque são o que **de fato** determina se seu agente de IA vai entregar coisa útil ou coisa frankenstein.

### O que cabe nessa camada

TDD (Test-Driven Development): escrever teste antes, e deixar o agente trabalhar contra o teste.

Testes automatizados em geral: unit, integration, e2e, contract, property-based.

Linters e formatters: ESLint, Ruff, Rubocop, SpotBugs, Checkstyle.

Análise estática: SonarQube, CodeQL, Semgrep.

Type checking estrito: TypeScript strict mode, mypy, Sorbet.

Code review disciplinado: humano ou com agente, mas com critério.

Arquitetura explícita: boundaries claras, dependências unidirecionais, domain modeling.

CI/CD com gates duros: build quebra se coverage cai, se lint falha, se teste vermelho.

Observabilidade do produto: logs, métricas, traces, feature flags.

Versionamento disciplinado: trunk-based, PRs pequenos, commits semânticos.

### Por que isso importa tanto agora

![](https://substackcdn.com/image/fetch/$s_!zsRW!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F025c38d6-f1ee-49b2-98bf-90ab6eaa8054_2150x1576.png)

O Fowler usa duas categorias que eu gosto: *guides* (feedforward) e *sensors* (feedback). Sensores computacionais pegam o troço estrutural com confiabilidade: código duplicado, complexidade ciclomática, cobertura de teste faltando, drift arquitetural, violações de estilo. São baratos, provados e determinísticos.

Repare na palavra: **determinísticos**. O modelo é probabilístico. A ferramenta é parcialmente determinística. As boas práticas de engenharia? Puro determinismo. Ou o teste passou ou não passou. Ou o linter reclamou ou não reclamou. Ou a coverage caiu ou não caiu.

**É aqui que você coloca o contrato que o LLM não pode furar.**

### O DORA 2025 não tá brincando

O relatório revela um insight central: a IA não conserta um time; ela amplifica o que já está lá. Times fortes usam a IA pra ficar ainda melhores e mais eficientes. Times que já patinavam vão descobrir que a IA só destaca e intensifica os problemas existentes.

Essa frase deveria estar colada no monitor de todo CTO. Deixa ela marinando.

A adoção de IA é quase universal: 90% dos respondentes da pesquisa reportam uso de IA no trabalho. Mais de 80% acreditam que ela aumentou sua produtividade. Entretanto, o ceticismo permanece: 30% reportam pouca ou nenhuma confiança no código gerado por IA.

E o recado mais pesado: sem sistemas de controle robustos, como testes automatizados fortes, práticas maduras de controle de versão, e loops rápidos de feedback, um aumento no volume de mudanças leva a instabilidade. Times trabalhando em arquiteturas frouxamente acopladas com loops rápidos de feedback veem ganhos, enquanto aqueles restritos por sistemas fortemente acoplados e processos lentos veem pouco ou nenhum benefício.

Ou seja: IA sem boas práticas é motor de Ferrari no chassi de Fusca. Roda, mas a primeira curva fecha o caixão.

### Exemplo do dia a dia: o mesmo task, dois cenários

![](https://substackcdn.com/image/fetch/$s_!RPpd!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F84a3e871-5287-4bfc-a100-7bb36ed79db2_2040x1496.png)

**Cenário A, só camada 1 e 2**: dev abre Claude Code, pede pra implementar um endpoint. Agente escreve. Dev lê, acha que tá bom, commita. Não rodou teste porque o projeto não tem teste. Não rodou linter porque não tem linter configurado. Em produção, bug em edge case. Perde duas horas debugando.

**Cenário B, camada 3 ativa**: dev abre Claude Code num projeto com TDD obrigatório, linter estrito, type check no CI. Pede pra implementar o endpoint. Agente escreve. Teste quebra em dois casos. Agente corrige. Linter aponta uma função com complexidade alta. Agente refatora. CI fica verde. Merge.

Mesma ferramenta. Mesmo modelo. Resultado completamente diferente. **A diferença tá na camada 3.**

É o que o Henrique Bastos vem argumentando no LinkedIn: o harness humano de práticas é o que mais pesa. É o que a Birgitta Böckeler e o Fowler chamam de “sensores computacionais” que são confiáveis porque determinísticos.

## O gradiente de controle: por que isso muda tudo

Olha pro desenho mental:

```markup
Camada 1 (Modelo)       ->  controle baixo  (você escolhe, e é isso)
Camada 2 (Ferramenta)   ->  controle medio  (você configura, estende)
Camada 3 (Engenharia)   ->  controle alto   (você escreve, define, audita)
```

O gradiente é real. E ele muda a conversa.

A maior parte do tempo e energia de quem tá debatendo AI coding hoje tá na camada 2. Fica todo mundo com vontade de falar de MCP, de sub-agent, de context engineering. Tudo isso importa. Mas é onde você tem **menos** alavanca por hora investida do que na camada 3.

Um dia estudando como configurar um AGENTS.md bem feito te dá ganho. Um dia escrevendo uma suite de testes sólida pro seu módulo crítico te dá ganho **muito maior**, porque esse ganho vira cerca pra qualquer LLM que entrar depois.

A camada 3 é investment capital. As outras duas são running cost.

## O mínimo que o engenheiro precisa masterizar agora

Se você é engenheiro e quer não virar refém de modelo ou de modismo, aqui vai o checklist honesto:

**1\. Saiba escrever teste antes do código.** TDD não é dogma, é ferramenta. Num mundo onde o LLM escreve código, o teste é a sua voz falando “não passa daqui”.

**2\. Domine linter e análise estática.** Configure bem. Rode no CI. Trave PR que falha. É sensor barato e determinístico.

**3\. Type system estrito.** TypeScript no strict. Python com mypy. Rust, Kotlin, Go. Use o sistema de tipos como documentação executável.

**4\. Arquitetura com fronteiras.** Dependências unidirecionais. Camadas explícitas. Domain boundaries. O LLM tende a embaralhar camadas; sua arquitetura precisa ser chata o suficiente pra ele não conseguir.

**5\. CI/CD com gates duros.** Coverage mínima. Lint obrigatório. Tipo obrigatório. Se quebrou, não passa. Sem exceção.

**6\. Code review com critério.** Seu ou de outro humano, ou de outro agente. Mas com critério. Não vai no “LGTM” automático.

**7\. Observabilidade de verdade.** Logs estruturados. Métricas de negócio. Traces distribuídos. Feature flags.

**8\. Disciplina de versionamento.** PR pequeno. Commit que fala. Trunk-based. Rollback fácil.

Nada disso é novo. É o que a gente já deveria estar fazendo há dez anos. A diferença é que agora, com o volume que o LLM consegue escrever, **não fazer** sai caríssimo.

## Fechando o devaneio

Augusto fechou o notebook frustrado. No dia seguinte, veio o Theo, tech lead do time. Sentou do lado dele e perguntou: *“cadê o teste?”*. Augusto disse que não tinha. Theo respondeu: *“então começa por aí, meu lindão. O Claude escreve. Mas quem diz o que é certo aqui é o teste. Não é ele, não é você.”*

Harness Engineering na acepção da literatura é importante. Vai continuar sendo. Saber escolher modelo importa, saber estender ferramenta importa.

Mas se você quer saber onde o bom engenheiro continua se destacando, e vai continuar se destacando nos próximos cinco anos, é na terceira camada. Onde mora o determinismo. Onde mora o contrato. Onde mora a disciplina.

A IA acelera. Quem define a direção continua sendo a engenharia de verdade. E ela não tá no Cursor. Tá no teste que você escreveu ontem.

A pergunta que fica: quanto do seu tempo tá indo pra camada 2 e quanto tá indo pra camada 3?

Se a resposta for “quase tudo na camada 2”, tem coisa errada no jogo.

---

*Esse texto nasceu de conversa com a galera sobre Harness Engineering. Vi que o termo tá virando um guarda-chuva grande demais, abraçando tudo que não é modelo. Achei que faltava alguém apontar o óbvio: a camada onde o engenheiro tem mais controle é a que menos gente tá olhando. Escrevi pra deixar isso claro.*

---

Se esse é um conteúdo que você acredita que pode ajudar alguém, clica no botão de compartilhar abaixo!

Agora se você quer mais conteúdos como esse na sua caixa de e-mail logo que saírem, é só assinar a newsletter.

---

### Fontes consultadas

¹ [METR (2025).](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/) *[Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/)*[. RCT com 16 desenvolvedores seniores em 246 tasks. Resultado: 19% mais lento com IA, apesar da percepção de 20% mais rápido.](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/)

² The Information, Wall Street Journal e TechCrunch. Dados financeiros OpenAI 2025: 8,67 bilhões em inferência nos primeiros 9 meses contra receita próxima de 4,3 bilhões no mesmo período. Declarações de Sam Altman sobre ChatGPT Pro.

³ Filing legal de março de 2026. CFO Krishna Rao declara “mais de 5 bilhões” em receita e “mais de 10 bilhões” em inferência e treinamento. Margem bruta negativa de 94% em 2024 (declaração pública de Dario Amodei).

⁴ DealBook Summit 2025. Declaração de Dario Amodei sobre “players YOLO” e risco de timing.

⁵ [DORA / Google Cloud (2025).](https://dora.dev/research/2025/dora-report/) *[State of AI-Assisted Software Development Report](https://cloud.google.com/blog/products/ai-machine-learning/announcing-the-2025-dora-report)*[. Pesquisa com quase 5.000 profissionais de tecnologia.](https://cloud.google.com/blog/products/ai-machine-learning/announcing-the-2025-dora-report)

⁶ [Fowler, M. & Böckeler, B. (2026).](https://martinfowler.com/articles/harness-engineering.html) *[Harness engineering for coding agent users](https://martinfowler.com/articles/harness-engineering.html)*[. martinfowler.com](https://martinfowler.com/articles/harness-engineering.html)

⁷ [Fowler, M. (2025).](https://martinfowler.com/articles/exploring-gen-ai/harness-engineering-memo.html) *[Harness Engineering, first thoughts](https://martinfowler.com/articles/exploring-gen-ai/harness-engineering-memo.html)*[. martinfowler.com](https://martinfowler.com/articles/exploring-gen-ai/harness-engineering-memo.html)

[⁸ LangChain (2026).](https://www.langchain.com/blog/the-anatomy-of-an-agent-harness) *[The Anatomy of an Agent Harness](https://www.langchain.com/blog/the-anatomy-of-an-agent-harness)*[.](https://www.langchain.com/blog/the-anatomy-of-an-agent-harness)

⁹ OpenAI. *Harness engineering: leveraging Codex in an agent-first world* (citado via Fowler).

¹⁰ Spotify Q4 2025 Earnings Call. Declarações de Gustav Soderstrom sobre migração pra Claude Code com Opus 4.5.

¹¹ [OpenCode (2026). Site oficial opencode.ai. 140 mil+ estrelas no GitHub, 6,5 milhões de devs mensais.](https://opencode.ai/)

¹² [Zechner, M. (2025).](https://mariozechner.at/posts/2025-11-30-pi-coding-agent/) *[What I learned building an opinionated and minimal coding agent](https://mariozechner.at/posts/2025-11-30-pi-coding-agent/)*[. mariozechner.at](https://mariozechner.at/posts/2025-11-30-pi-coding-agent/)

**Links completos:**

- https://www.anthropic.com/engineering/harness-design-long-running-apps
- https://blog.arcade.dev/ai-inference-economics
- https://www.wheresyoured.at/why-are-we-still-doing-this/