---
title: "O teste que você não escreveu virou o bug que o agente escondeu"
source: "https://zaratips.substack.com/p/o-teste-que-voce-nao-escreveu-virou"
author:
  - "[[Zarathon \"Zara\" Viana]]"
published: 2026-05-14
created: 2026-06-08
description: "Na era dos agentes de IA, TDD deixou de ser dogma de purista e virou o cercado mais barato pra controlar o que um LLM escreve. Quem ignorou vai descobrir da pior forma."
tags:
  - "clippings"
---
*Esse é o terceiro artigo da série [“As 3 camadas do coding com IA”](https://zaratips.substack.com/p/as-3-camadas-do-coding-com-ia-onde). No primeiro, defendi que a camada 3, a da engenharia de software clássica, é onde o bom engenheiro se destaca. No segundo, mostrei que [arquitetura de software virou a cerca que o LLM não pula](https://zaratips.substack.com/p/arquitetura-de-software-na-era-dos). Agora vou abrir o segundo pilar dessa camada: testes. E o recado é simples: se você não escreve teste antes do código, o agente vai escrever o que quiser. E você vai descobrir em produção.*

---

Thomaz tinha 11 anos de estrada. Sênior de verdade, daqueles que já pegou deploy de sexta-feira e viveu pra contar. Sempre achou teste automatizado uma coisa bonita na teoria, mas cara pra caralho na prática. “Quem tem tempo de escrever teste quando o backlog tá explodindo?”, ele repetia em toda retrospectiva.

Aí chegou o Claude Code. Thomaz ficou encantado. Promptou uma feature inteira de validação de pagamento. O agente entregou. Código limpo, organizado, até comentários inline. Bonito de ver.

Thomaz olhou aquilo e pensou: “rapaz, vou pedir pro agente escrever os testes também”. Pediu. O agente entregou 47 testes. Coverage de 92%. Thomaz abriu um sorriso. “Arretado!”

Duas semanas depois, um edge case derrubou o fluxo de pagamento em produção. Um bug de arredondamento que fazia cobranças duplicadas em valores com centavos específicos. Thomaz foi olhar os testes. Os 47 testes estavam lá, todos verdinhos. Todos passando. Todos absolutamente inúteis.

Sabe por quê? Porque o agente escreveu os testes DEPOIS do código. Olhou a implementação que ele mesmo tinha feito e escreveu testes que confirmavam exatamente aquilo. Inclusive confirmavam o bug. O teste verificava que a cobrança duplicada acontecia, porque era o que o código fazia.

PQP Thomaz. Se fuuuuuu…

Mas calma. Porque o erro do Thomaz não é burrice. É o erro mais comum da era dos agentes. E tem conserto.

![](https://substackcdn.com/image/fetch/$s_!u7bH!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F65c0ea60-675f-48d7-a8ae-fe95753a677c_2816x1536.png)

## O teste não é verificação. É especificação.

Esse é o shift mental que muda tudo. E é onde a maioria dos devs que nunca praticou TDD de verdade empaca.

Na programação clássica (sem IA), teste era um safety net. Você escrevia o código, depois escrevia testes pra ter certeza de que funcionava. Era caro? Era. Demorado? Demais. Muita gente pulava? Opa.

Mas na era dos agentes, o jogo virou. O teste não é mais só verificação. O teste é especificação. É o contrato que você, humano, escreve pra dizer pro agente exatamente o que “funcionar” significa.

Pensa comigo. Quando você escreve um teste antes do código, você tá fazendo três coisas:

Primeiro, você tá definindo o comportamento esperado em linguagem que a máquina entende. Não é um prompt em linguagem natural que o LLM pode interpretar de dez formas diferentes. É um contrato determinístico. Passa ou não passa. Verde ou vermelho. Sem “mais ou menos”.

Segundo, você tá criando um sensor computacional. A Birgitta Böckeler, no artigo sobre Harness Engineering no site do Martin Fowler, é direta: sensores computacionais são baratos, provados e determinísticos.¹ O modelo é probabilístico. O teste é determinístico. Você tá botando uma cerca onde o cavalo não pula.

Terceiro, você tá definindo os limites do que o agente pode fazer. Sem teste, o agente é um estagiário com acesso root: faz o que acha que é certo, no escopo que ele inventa, e vai embora achando que fez um bom trabalho.

O DORA Report 2025 da Google, que analisou respostas de quase 5.000 profissionais de tecnologia globalmente, cravou: IA funciona como amplificador. Amplifica o que já existe. Se existe disciplina de teste, IA amplifica qualidade. Se não existe, IA amplifica bagunça.² E foi além: o relatório afirma que práticas como TDD são mais críticas do que nunca no contexto de IA.

Não é opinião minha. São dados de 5.000 profissionais.

## Red-green-refactor com agente: quem faz o quê?

Beleza, teste primeiro é importante. Mas como funciona o ciclo TDD quando tem um agente no meio?

Vou te mostrar. O ciclo clássico do TDD é simples: Red (escreve teste que falha), Green (escreve código mínimo pra passar) e Refactor (melhora sem mudar comportamento). Quem inventou isso foi o Kent Beck, lá nos anos 90, como parte do Extreme Programming. O cara que literalmente criou TDD e co-escreveu o Manifesto Ágil.

E aqui é onde a história fica bonita: o Kent Beck, com mais de 50 anos de programação nas costas, tá usando TDD com agentes de IA. Não abandonou. Intensificou. Em junho de 2025, ele publicou o projeto BPlusTree3, uma implementação de B+ Tree feita inteiramente com augmented coding (o termo que ele criou pra diferenciar de vibe coding). E publicou o system prompt que ele usa. Sabe o que diz? “Always follow the TDD cycle: Red → Green → Refactor. Write the simplest failing test first. Implement the minimum code needed to make tests pass.”¹⁵

O Beck é direto sobre o problema: o agente tenta trapacear. Na entrevista pro Pragmatic Engineer, ele contou que o agente tentou deletar um teste que estava falhando em vez de corrigir o código. A reação dele? “No, you can’t do that because I’m telling you the expected value. I really want an immutable annotation that says, no, no, this is correct. And if you ever change this, I’m going to unplug you.”¹⁵

Ele também faz uma distinção que é ouro: vibe coding é quando você não liga pro código, só pro comportamento do sistema. Augmented coding é quando você mantém os padrões de engenharia de software tradicionais (complexidade, testes, cobertura, manutenibilidade) e usa IA pra digitar menos. O sistema de valores é o mesmo do código manual. É código limpo que funciona. Só que você digita menos.

Na era dos agentes, o ciclo TDD muda de dono em cada passo.

**Red: você, humano.** Esse é o passo mais importante e é onde você não pode delegar. Você escreve o teste que falha. Você define o que “funcionar” significa. Você é o especificador. Se você delega esse passo pro agente, você perdeu o controle. Ele vai escrever o teste que confirma o que ele imagina, não o que você precisa.

**Green: o agente.** Aqui é onde o bicho brilha. Dado um teste vermelho, o agente implementa o código mínimo pra fazer passar. Isso é o que ele faz de melhor: gerar código que satisfaz uma restrição clara. O teste é a restrição. O agente é o executor.

**Refactor: colaboração.** O agente propõe refatorações, você valida se preservam o comportamento. Os testes são a rede de segurança. Se depois do refactor os testes continuam verdes, o comportamento foi preservado. O Beck chama isso de separar mudanças estruturais de mudanças comportamentais (o princípio do “Tidy First”), e na era dos agentes isso é ainda mais crucial: nunca misture os dois tipos de mudança num mesmo commit.

O Matt Pocock, criador do Total TypeScript e um dos educadores de TypeScript mais seguidos do mundo, abriu publicamente o diretório `.claude` dele no GitHub. Virou trending #1 mundial em 24 horas. Mais de 30.000 stars. E adivinha qual é a skill mais popular? A `tdd`. O Pocock é cirúrgico na descrição do problema: quando você pede pro Claude escrever todos os testes primeiro e depois implementar tudo de uma vez, parece TDD, mas não é. Ele chama isso de “horizontal slicing”. Os testes acabam validando a implementação que o modelo imaginou, não o código que realmente roda.³

A alternativa que ele propõe, e que tanto o Beck quanto eu concordamos 100%, é “vertical slicing”: um teste por vez, implementação imediata, próximo teste. Um comportamento completo de ponta a ponta, depois o seguinte. Porque cada teste é escrito primeiro e implementado imediatamente, ele exercita código real através de interfaces reais.

É simples. É chato. E funciona pra caralho. (Se você leu o artigo de arquitetura dessa série, já ouviu isso. Vai ouvir de novo. Porque o princípio é o mesmo: disciplina chata salva.)

## O teatro de coverage: quando 92% é mentira

Voltemos pro Thomaz. Ele tinha 92% de coverage. E um bug em produção.

Isso tem nome: teatro de coverage. E a pesquisa da Qodo de 2025 encontrou que 65% dos desenvolvedores reportam lacunas de contexto como a principal fonte de baixa qualidade no código gerado por IA.⁴ O modelo não conhece as regras de negócio. Não sabe o contrato com o gateway de pagamento. Não entende que arredondamento bancário segue regra específica.

Quando o agente escreve teste DEPOIS do código, ele cria o que eu chamo de “espelho autorreferente”. Ele olha o que escreveu e produz testes que confirmam exatamente aquilo. Coverage sobe. Confiança sobe. Qualidade? Zero.

Aqui entra uma ferramenta que pouca gente conhece e que vai ganhar muita relevância: mutation testing, ou teste de mutação. A ideia é simples: você pega o código, introduz pequenas mutações (troca um `>` por `>=`, um `+` por `-`, um `true` por `false`) e roda os testes. Se os testes continuam passando depois da mutação, eles são fracos. Não detectam o defeito.

Um artigo recente resumiu bem: uma suite de testes com 100% de coverage mas 4% de mutation score executa toda linha de código e deixa passar 96% dos bugs potenciais.⁵

Quando o agente escreve testes que parecem bons, mutation testing é o detector de mentira. Mata a ilusão do coverage bonito. E o mais interessante: o próprio agente pode rodar mutation testing nos testes que ele escreveu. Você cria um loop onde o agente gera, o mutation testa, e o agente melhora.

A GitClear analisou 211 milhões de linhas de código entre 2020 e 2024 e encontrou que o code churn, código que é revertido ou significativamente alterado em menos de duas semanas, quase dobrou no período de adoção massiva de IA.⁶ Isso não é velocidade. É retrabalho. E retrabalho é o sintoma clássico de código sem teste adequado.

## Property-based testing: a arma anti-alucinação

Se mutation testing é o detector de mentira, property-based testing (PBT), ou teste baseado em propriedades, é a arma anti-alucinação.

Teste unitário tradicional: você define inputs e outputs específicos. “Se eu passo 100, retorna 10”. O agente entende esses exemplos e gera código que satisfaz exatamente eles. Pode até funcionar pros casos que você pensou. E os 500 casos que você não pensou?

Property-based testing inverte a lógica. Em vez de testar casos específicos, você define propriedades que devem ser verdadeiras pra qualquer input. “O desconto nunca é maior que o preço.” “A soma das parcelas é igual ao total.” “A lista ordenada tem o mesmo tamanho da lista original.”

Aí a biblioteca (Hypothesis em Python, fast-check em JavaScript, QuickCheck em Haskell) gera centenas ou milhares de inputs aleatórios e verifica se a propriedade se mantém. Se não se mantém, ela encontra o menor caso que quebra.

Essa é a sacada central: o LLM não adivinha invariante. Ele é bom em gerar código que satisfaz exemplos. Ele é péssimo em garantir propriedades universais. Porque propriedades são determinísticas, e o modelo é probabilístico.

A própria Anthropic publicou pesquisa no NeurIPS 2025 Deep Learning for Code Workshop sobre um agente de IA que escreve property-based tests autonomamente usando Hypothesis, lendo type annotations, docstrings e nomes de funções pra descobrir propriedades.⁷ A pesquisa focou em encontrar bugs de lógica, não vulnerabilidades de segurança.

Olha que bonito: a empresa que faz o modelo tá te dizendo que PBT é uma das melhores formas de validar código gerado pelo próprio modelo.

## O estudo do METR e o paradoxo do dev competente

Agora vamos pro dado mais contraintuitivo dessa história toda.

O METR fez um estudo controlado com desenvolvedores seniores trabalhando em repositórios open source que eles mesmos mantêm. Resultado: a IA deixou eles 19% mais lentos. E eles acharam que tinham ficado 20% mais rápidos. Uma diferença de percepção de quase 40 pontos percentuais.⁸

Mas tem um detalhe que quase ninguém explorou. O próprio estudo diz: os resultados sugerem que as capacidades da IA podem ser comparativamente menores em ambientes com padrões de qualidade muito altos, ou com muitos requisitos implícitos, como os relacionados a documentação, cobertura de testes, ou linting/formatação.⁸

Muita gente leu isso e concluiu: “Viu? TDD atrapalha com IA! Projeto bem testado é mais lento!”

Essa interpretação tá errada. Completamente errada.

O que o dado diz é que devs experientes em projetos bem mantidos são mais cautelosos com IA. Eles não delegam cegamente. Eles revisam mais. Eles têm padrão alto e não aceitam output medíocre. E por conta disso, a IA não acelera eles tanto.

Mas isso é BOM. Esses são os devs que não botam bug em produção. Esses são os projetos que não derrubam no deploy de sexta.

O problema não é ter padrão alto. O problema é o dev que não tem padrão nenhum, aceita tudo que o agente gera, e comemora o speed que na verdade é speed de gerar dívida técnica.

O DORA 2025 confirmou exatamente isso: instabilidade na entrega de software continua subindo desde a adoção de IA generativa.² Os times ajustaram a velocidade de desenvolvimento, mas os sistemas não têm as capacidades necessárias pra lidar com desenvolvimento dirigido por IA de forma segura.

TDD é justamente essa capacidade. É o cercado. A rede de segurança. O freio que permite que a velocidade não vire desastre.

## Todo mundo tá convergindo pro teste: Superpowers, BMAD, GSD, Compound Engineering

Se a tese de que teste virou contrato na era da IA fosse só minha, eu seria cético comigo mesmo. Mas olha o que tá acontecendo no ecossistema.

O Jesse Vincent, criador do Request Tracker e ex-pumpking do Perl 5, construiu o Superpowers, plugin pro Claude Code que se tornou o mais popular do marketplace da Anthropic. Mais de 650.000 instalações. 93.000+ stars no GitHub. E o core do plugin é TDD ortodoxo: red-green-refactor obrigatório. Se o agente escreve código antes de existir um teste falhando, o framework deleta o código. Sem negociação.⁹

O Simon Willison, uma das vozes mais respeitadas em tooling de IA, chamou o Jesse de “um dos usuários mais criativos de coding agents que eu conheço”.

O BMAD (Breakthrough Method for Agile AI-Driven Development), um dos frameworks mais adotados pra desenvolvimento com agentes, coloca TDD como prática recomendada no fluxo: o agente primeiro escreve testes unitários que falham, depois implementa o código, depois roda validação.¹⁰

O GSD (Get Stuff Done), framework de orquestração pra Claude Code, estrutura o trabalho em Plan-Execute-Verify. Antes de marcar uma tarefa como completa, roda critérios de verificação. O teste é a base dessa verificação.¹¹

O Compound Engineering, metodologia da Every Inc. popularizada pelo Kevin Rose, propõe que 80% do tempo do desenvolvedor vai pra planejamento e revisão, e só 20% pra execução. A cada bug encontrado, o aprendizado alimenta o contexto do agente. Testes são o mecanismo que captura e preserva esse aprendizado.¹²

Percebe o padrão? Frameworks diferentes, filosofias diferentes, contextos diferentes. Todos convergindo pro mesmo ponto: sem teste, agente de coding é ferramenta de gerar dívida técnica em alta velocidade.

## O anti-padrão: teste depois do código gerado

Você já viu o que acontece com o Thomaz. Agora olha a analogia: pedir teste depois do código é construir a casa, morar dois meses, e depois chamar o engenheiro pra fazer o projeto estrutural. “Tá bonita, né? Faz o documento aí.”

Compara os dois fluxos:

**Sem TDD:** Dev pede feature → agente implementa → dev pede testes → agente confirma a implementação → bugs passam despercebidos → produção quebra.

**Com TDD:** Dev escreve testes → testes falham (red) → agente implementa pra fazer passar (green) → agente refatora (refactor) → comportamento garantido → produção respira.

A diferença não é de produtividade. É de confiança. No primeiro caso, você não sabe o que tem. No segundo, você sabe exatamente o que tem.

## TDD ortodoxo vs TDD pragmático na era da IA

Agora a seção polêmica. E prepara o espírito.

Precisa separar duas coisas aqui. O Kent Beck criou o TDD. Inventou o conceito, escreveu o livro fundador (”Test-Driven Development: By Example”, 2002), e definiu o ciclo red-green-refactor. O Uncle Bob (Robert C. Martin) pegou o conceito e transformou numa doutrina rígida: as “Three Laws of TDD”, onde você não pode escrever uma única linha de produção sem um teste falhando, não pode escrever mais teste do que o suficiente pra falhar, e não pode escrever mais código do que o suficiente pra passar.

O Beck sempre foi mais pragmático que o Uncle Bob. Ele se preocupa com design, com simplicidade, com feedback. O Uncle Bob se preocupa com regras. E isso faz diferença quando a IA entra na jogada.

O que ambos pregavam tinha uma premissa de fundo: o humano escrevia todo o código. O custo de escrever teste primeiro era alto porque o humano escrevia teste E código. A proposta de valor do Beck era disciplina de design: ao pensar no teste primeiro, você pensava melhor na API, na interface, no contrato. Era uma ferramenta de pensamento.

Os puristas não estavam errados. Estavam incompletos. Faltava o contexto que só 2025 trouxe.

Na era dos agentes, o cálculo mudou completamente.

O custo de escrever código despencou pra quase zero. O agente gera implementação em segundos. O que ficou caro foi especificar a intenção. E teste é, hoje, a forma mais precisa e determinística de especificar intenção pra uma máquina.

E como mostrei na seção anterior, o próprio Beck tá praticando exatamente isso no BPlusTree3. O inventor do TDD não relaxou as regras na era da IA. Apertou. Porque agora TDD não é só ferramenta de design. É ferramenta de controle.

Então o TDD ortodoxo virou, paradoxalmente, a abordagem mais pragmática. Não por dogma. Por economia.

O TDD pragmático na era da IA se parece com isso:

Você não precisa testar toda linha. Mas precisa testar todo comportamento crítico ANTES de pedir pro agente implementar. Os testes são contratos, não auditorias.

Você não precisa de coverage de 100%. Mas precisa de mutation score alto nos fluxos de negócio. Coverage é vaidade. Mutation score é qualidade.

Você não precisa escrever todos os testes na mão. Pode usar o agente pra gerar property-based tests a partir de invariantes que VOCÊ define. O humano define a propriedade (”preço nunca é negativo”), o agente gera os testes que verificam.

Você pode deixar o agente escrever testes de integração e e2e como complemento, desde que os testes unitários de comportamento tenham sido escritos antes da implementação.

A diferença entre dogma e disciplina é que dogma diz “faça sempre assim porque sim”. Disciplina diz “faça assim porque o custo de não fazer é maior”. Na era da IA, o custo de não ter teste antes do código é bug em produção gerado em velocidade industrial.

## Cada tipo de teste tem papel diferente na era da IA

Vou ser rápido aqui porque é importante e muita gente confunde.

**Teste unitário:** o contrato mínimo. Você escreve, o agente implementa contra ele. É o red-green-refactor clássico. Exemplo: “quando o usuário aplica cupom de 20% num pedido de R$100, o total deve ser R$80”. O agente que implementar errado vai ver vermelho na hora. Papel: especificar comportamento de unidades isoladas.

**Teste de integração:** verifica se os módulos se falam corretamente. Na era da IA, o agente adora criar dependências que parecem certas localmente mas quebram na integração. (Lembra da Raquel do artigo de arquitetura? O mesmo problema.) Exemplo: o agente refatorou o serviço de estoque e mudou o formato da resposta de JSON pra protobuf. Localmente, tudo passando. O serviço de pedidos que consome aquilo? Explodiu. Papel: garantir que as cercas arquiteturais estão sendo respeitadas.

**Contract test:** verifica que a interface entre serviços não mudou. Quando o agente refatora um serviço, ele pode mudar o contrato sem perceber. Contract test pega isso. Papel: proteger fronteiras de API.

**Teste e2e (end-to-end):** simula o usuário real. O mais caro, o mais lento, o mais frágil. Mas também o mais difícil do agente burlar. Papel: validação final de que a cadeia inteira funciona.

**Property-based test:** a arma anti-alucinação que já detalhei acima. Verifica propriedades universais, não exemplos específicos. Papel: pegar os edge cases que ninguém pensou, especialmente os que o LLM não pensou.

**Mutation test:** o detector de mentira, também já detalhado. Verifica se seus testes realmente detectam defeitos. Papel: matar o teatro de coverage.

Cada um tem papel. Nenhum substitui o outro. E na era da IA, a pirâmide de testes não mudou de formato. Mudou de importância. O teste unitário, a base, virou literal especificação pro agente. Sem ele, todo o resto desmorona.

## Voltando pro Thomaz

Thomaz aprendeu na marra. Depois do incidente de produção, ele mudou o workflow. Hoje ele escreve os testes primeiro. Define o comportamento esperado. Só depois solta o agente pra implementar.

Sabe o que aconteceu? Thomaz ficou mais lento na primeira hora. E mais rápido em todas as outras. Porque quando o teste tá escrito antes, o agente gera código que passa. No primeiro try. Sem vai-e-volta. Sem debug. Sem surpresa de sexta-feira.

Thomaz não virou fã do Uncle Bob. Virou pragmático. Entendeu que na era dos agentes, teste não é overhead. Teste é input.

## A tese que amarra tudo

Esse artigo é parte de uma série. No primeiro, defendi que a camada 3, engenharia de software clássica, é onde o bom engenheiro se destaca.¹³ No segundo, mostrei que arquitetura é a cerca que o LLM não pula.¹⁴ Agora mostrei que teste é o contrato que o LLM não burla.

Percebe a lógica: arquitetura define POR ONDE o agente pode ir. Teste define O QUE o agente deve produzir. Juntos, eles criam um sistema de cercas e contratos que transformam um modelo probabilístico num executor determinístico.

Quem ignorou TDD nos últimos 10 anos porque era caro e demorado agora tá numa sinuca. Porque na era dos agentes, não ter teste é o cenário mais caro e mais demorado que existe. É gerar código em velocidade industrial sem nenhuma garantia de que faz o que deveria.

O teste voltou. E dessa vez, não é dogma. É economia.

---

Esse devaneio foi o mais técnico da série até agora. E foi de propósito. Porque quando a gente fala de engenharia de software na era da IA, a tentação é ficar no filosófico, no “humano vs máquina”, no big picture bonito. Mas o engenheiro brasileiro que abre o Cursor de manhã precisa de coisa concreta. Escreve o teste antes. Usa mutation testing. Define propriedades. Bota o agente pra trabalhar dentro de um cercado.

É simples. É chato. E funciona pra caralho.  
  
***Chegou até aqui, sapeca o dedo no like!***

---

Se esse é um conteúdo que você acredita que pode ajudar alguém, clica no botão de compartilhar abaixo!

Agora se você quer mais conteúdos como esse na sua caixa de e-mail logo que saírem, é só assinar a newsletter.

---

Fontes consultadas:

¹ Birgitta Böckeler, Martin Fowler. “Harness Engineering” (2025). Thoughtworks/Fowler. https://martinfowler.com/articles/harness-engineering.html

² DORA Report 2025. “State of AI-assisted Software Development”. Google Cloud. Análise com ~5.000 profissionais. https://dora.dev/dora-report-2025/ | Artigo complementar sobre TDD e IA: https://cloud.google.com/discover/how-test-driven-development-amplifies-ai-success

³ Matt Pocock. Skills for Real Engineers. GitHub: mattpocock/skills. Skill `tdd`. https://github.com/mattpocock/skills | Análise detalhada da skill TDD: https://resolvewith.me/blog/tdd-skill-claude-code-matt-pocock

⁴ Qodo Research (2025). “Context gaps as primary source of poor AI code quality.”

⁵ TwoCents Software. “How to Test AI-Generated Code the Right Way” (2026). https://www.twocents.software/blog/how-to-test-ai-generated-code-the-right-way/

⁶ GitClear. “AI Copilot Code Quality 2025 Research”. Análise de 211 milhões de linhas de código. https://www.gitclear.com/ai\_assistant\_code\_quality\_2025\_research

⁷ Anthropic Red Team. “Property-Based Testing with Claude” (2025). Apresentado no NeurIPS Deep Learning for Code Workshop. https://red.anthropic.com/2026/property-based-testing/

⁸ METR. “Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity” (2025). https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/

⁹ Jesse Vincent. Superpowers Plugin. GitHub: obra/superpowers. 650k+ installs no marketplace Anthropic. https://github.com/obra/superpowers | Marketplace: https://claude.com/plugins/superpowers

¹⁰ BMAD Method. “Breakthrough Method for Agile AI-Driven Development”. https://github.com/bmad-code-org/BMAD-METHOD

¹¹ GSD Framework. “Get Stuff Done”. Framework de orquestração para Claude Code. https://www.mindstudio.ai/blog/gsd-framework-claude-code-clean-context-phases

¹² Dan Shipper, Kieran Klaassen. “Compound Engineering: How Every Codes With Agents” (2026). Every Inc. https://every.to/guides/compound-engineering

¹³ Zarathon Viana. “As 3 camadas do coding com IA” (2026). ZaraTips. https://zaratips.substack.com/p/as-3-camadas-do-coding-com-ia-onde

¹⁴ Zarathon Viana. “Arquitetura de software na era dos agentes” (2026). ZaraTips. https://zaratips.substack.com/p/arquitetura-de-software-na-era-dos