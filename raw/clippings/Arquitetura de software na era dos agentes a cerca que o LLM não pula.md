---
title: "Arquitetura de software na era dos agentes: a cerca que o LLM não pula"
source: "https://zaratips.substack.com/p/arquitetura-de-software-na-era-dos"
author:
  - "[[Zarathon \"Zara\" Viana]]"
published: 2026-05-06
created: 2026-06-08
description: "Se você sempre achou Clean Architecture exagero, vai ter que rever. Não pelo motivo que os puristas defendiam. Por um motivo novo: o LLM precisa de cerca."
tags:
  - "clippings"
---
*Esse é o segundo artigo da série [“As 3 camadas do coding com IA”](https://zaratips.substack.com/p/as-3-camadas-do-coding-com-ia-onde). No primeiro, defendi que a camada 3, a da engenharia de software clássica, é onde o bom engenheiro se destaca na era da IA. Agora vou abrir um dos pilares dessa camada: arquitetura de software. E o recado é simples: se a sua arquitetura não é explícita, o agente vai fazer a festa. E você vai limpar a bagunça.*

---

Raquel tinha 6 anos de experiência. Backend sólido, boas práticas, code review rigoroso. O tipo de engenheira que você quer no seu time quando o bicho pega em produção.

Ela entrou num time novo. Monorepo grande, uns 200 mil linhas de código. Nenhum documento de arquitetura (quem nunca). Nenhuma regra de dependência explícita. Os módulos se importavam uns aos outros sem cerimônia nenhuma. Tipo festa de São João sem cerca: todo mundo entra e sai por onde quer.

Raquel ligou o Claude Code, deu contexto do que precisava, e mandou bala.

O agente entregou. Código funcionando. Testes passando. PR aberto.

Dois dias depois, o deploy derrubou o serviço de pagamentos. Por quê? Porque o agente, pra resolver o problema que Raquel pediu, criou uma dependência circular entre o módulo de pedidos e o módulo de pagamentos. Importou um helper de pagamentos direto dentro da camada de domínio de pedidos. E ninguém percebeu no review porque o código tava bonito, os testes passaram e a lógica local fazia sentido.

O problema não era local. O problema era global. E o LLM não pensa global. E você achando que só você manjava de gambiarra, né?!

Azedou, Raquel se lascou e nem conseguia entender o que tinha acontecido ao certo. Mas calma. Porque a história tem uma segunda parte.

![](https://substackcdn.com/image/fetch/$s_!_j_S!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F181a42f1-a2f3-444a-be35-b6ac03da0aa9_2816x1536.png)

## Por que o LLM embaralha camadas (e você nem percebe)

![](https://substackcdn.com/image/fetch/$s_!2bgD!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7c0c9577-a127-489c-b9ff-1013435d8bdf_1165x855.png)

Vamos falar a real: o LLM é absurdamente bom em resolver problemas locais. Você dá um arquivo, uma classe, uma função, e ele resolve. Às vezes melhor do que você resolveria.

O problema é que software não é uma coleção de problemas locais. Software é um sistema. E sistema tem fronteiras. Tem contratos. Tem direções de dependência. Tem coisas que podem se falar e coisas que não podem.

O LLM não sabe disso. Ele não leu o diagrama de arquitetura que tá na cabeça do tech lead (ou, pior, que não tá escrito em lugar nenhum). Ele faz o que parece mais lógico no contexto que ele tem. E o que parece mais lógico localmente quase sempre é pegar o atalho.

Precisa de um helper que tá em outro módulo? Importa direto. Precisa de um tipo que tá na camada de infra? Puxa pra dentro do domínio. Precisa de uma constante de configuração? Referencia o módulo de config direto no use case.

Cada uma dessas decisões, isoladamente, faz sentido. O código compila. Os testes passam. O reviewer olha e pensa: “tá limpo, tá bonito, LGTM”.

Só que cada atalho desse é um fio a mais no emaranhado. E quando você acumula 50, 100, 200 desses atalhos, o que era um sistema com fronteiras vira uma bola de lama (big ball of mud).

A Birgitta Böckeler, no artigo sobre harness engineering publicado no site do Fowler, é direta: sensores computacionais pegam problemas estruturais com confiabilidade. Código duplicado, complexidade ciclomática, cobertura de teste faltando, drift arquitetural, violações de estilo. São baratos, provados e determinísticos.¹

Percebe a palavra: **determinísticos**. O modelo é probabilístico. A arquitetura precisa ser determinística. Ou a dependência é permitida ou não é. Ou a camada respeita a fronteira ou não respeita. Não tem “provavelmente respeita”.

## Clean Architecture e Hexagonal: de “exagero” a necessidade

Vou ser direto com você: eu já achei Clean Architecture overengineering pra boa parte dos projetos. Aquele monte de camada, interface, adapter, port, use case, entity. Pra um CRUD? Parecia canhão pra matar formiga (e é em muitos casos).

Mas como já dizia Raul, “Eu prefiro seeeeeerrrrr, essa metamorfose ambulante…” Mudei de ideia. Não pelos motivos que os puristas sempre defenderam (desacoplamento por princípio, testabilidade pura, blá blá blá). Mudei por um motivo novo e muito mais pragmático: o LLM precisa de cerca.

Quando você tem uma arquitetura hexagonal ou uma Clean Architecture implementada de verdade, com camadas explícitas e direção de dependência definida, acontece uma coisa mágica: o agente não tem pra onde ir. Ele não consegue importar infra dentro do domínio porque o linter barra. Ele não consegue criar dependência circular porque o ArchUnit (ou o dependency-cruiser, se for JavaScript) explode o CI. Estou citando esses modelos porque são os mais famosos, mas existem outros tantos igualmente bons, os mais velhos vão lembrar do MVC/MTV do rails/django.

A arquitetura chata virou a melhor amiga do coding com IA. Isso me lembrou esse [artigo](https://mcfunley.com/choose-boring-technology) de 2015.

Pensa assim: toda vez que você define uma regra arquitetural explícita e bota um sensor pra checar, você tá criando uma cerca. O LLM pode ser um cavalo potente, mas cavalo com cerca não pula pro pasto do vizinho.

O Fowler e a Böckeler chamam isso de “architecture fitness harness”, a parte do harness que define e checa as características arquiteturais da aplicação. Basicamente: fitness functions.¹ Testes de arquitetura que rodam no CI e barram qualquer violação antes dela chegar na main.

É simples. É chato. E funciona pra caralho.

## DDD, bounded contexts e linguagem ubíqua: os “guides” do agente

Agora vamos pro Eric Evans. Domain-Driven Design. DDD.

![](https://substackcdn.com/image/fetch/$s_!S4WJ!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F36831af2-2b48-4bfc-aa95-2b01deacf2d7_1600x992.png)

Muita gente trata DDD como coisa acadêmica, coisa de livro grosso, coisa de consultoria cara. Mas no mundo dos agentes de coding, três conceitos do DDD viraram absurdamente práticos.

### Bounded contexts como cercas semânticas

Um bounded context é uma fronteira explícita onde um modelo de domínio específico se aplica. “Pedido” no contexto de vendas é diferente de “Pedido” no contexto de logística. Cada contexto tem suas regras, suas entidades, seus contratos.

Quando você define bounded contexts explícitos e materializa eles na estrutura do código (pastas, módulos, pacotes), o agente ganha um mapa. Ele sabe onde tá. Ele sabe o que pertence aqui e o que não pertence. E quando ele tenta cruzar a fronteira, o sensor computacional barra.

O Russ Miles, no Engineering Agents, coloca assim: com DDD aplicado, o agente sabe a diferença entre “claim” e “ticket”, entre “approval” e “authorisation”. Ele fala o dialeto do seu negócio, não o inglês genérico de pitch deck do Vale do Silício.²

Isso é poder. E é poder que vem de decisão de arquitetura, não de prompt engineering.

### Linguagem ubíqua como contexto pro LLM

Aqui é onde a coisa fica realmente quente.

A linguagem ubíqua, o vocabulário compartilhado entre devs, product, domínio, e agora o agente, funciona como contexto semântico de altíssima qualidade. Quando o time inteiro (humano e máquina) usa os mesmos termos, o LLM não inventa nomes. Não cria abstrações fantasma. Não chama de “item” o que deveria ser “reserva”.

Daniel Schleicher defende isso com dados: quando todo o time, incluindo agentes de IA, compartilha um entendimento explícito do que “pedido” significa no contexto de gestão de pedidos, classes inteiras de erros arquiteturais se tornam impossíveis.³

Pensa no impacto disso. Você bota um glossário de domínio no `CLAUDE.md` ou no `AGENTS.md`. O agente lê. E a partir dali, toda vez que ele escreve código, ele usa os termos certos. Não porque ele entende o negócio. Mas porque ele tem uma cerca linguística que canaliza ele pro vocabulário correto.

DDD sempre foi sobre comunicação. Agora é sobre comunicação entre humano e máquina. O Evans não tinha como prever isso, mas acertou em cheio.

### Aggregates como unidades de mudança

Vou tocar rápido nesse ponto porque é importante. Um aggregate no DDD é uma unidade de consistência. Tudo que muda junto vive junto. O aggregate root é o ponto de entrada. Ninguém de fora mexe no miolo sem passar pelo root.

Pra um agente de coding, aggregate é ouro. Ele sabe: “se eu preciso mudar algo nessa entidade, eu entro pelo aggregate root”. Ele não sai mexendo em qualquer lugar. A fronteira de transação tá definida. O escopo de mudança tá contido.

Aggregate mal definido = agente fazendo cirurgia em órgão errado.

## Dependências unidirecionais: sensor computacional pra drift arquitetural

Ok, você definiu camadas. Definiu bounded contexts. Definiu linguagem ubíqua. Lindo no diagrama.

Mas como garante que na prática o agente (e os devs humanos também, diga-se) vão respeitar essas fronteiras?

Resposta: sensor computacional. Ferramentas que checam direção de dependência automaticamente, no CI, em cada PR, sem exceção. Ou se você quiser, configura pra rodar local também.

**Em Java: ArchUnit.** Você escreve testes de arquitetura que rodam como JUnit. Um exemplo simples:

```markup
layeredArchitecture()
    .consideringAllDependencies()
    .layer("Controllers").definedBy("..controller..")
    .layer("Services").definedBy("..service..")
    .layer("Repositories").definedBy("..repository..")
    .whereLayer("Controllers").mayNotBeAccessedByAnyLayer()
    .whereLayer("Services").mayOnlyBeAccessedByLayers("Controllers")
    .whereLayer("Repositories").mayOnlyBeAccessedByLayers("Services")
    .check(classes);
```

Se algum código, escrito por humano ou por agente, tentar importar um repositório direto de um controller, o build quebra. Ponto. Sem discussão. Sem “ah, mas nesse caso faz sentido”. Não passa.⁴

**Em JavaScript/TypeScript: dependency-cruiser.** Mesma ideia, config diferente:

```markup
{
  "forbidden": [
    {
      "name": "no-domain-to-infra",
      "severity": "error",
      "from": { "path": "^src/domain" },
      "to": { "path": "^src/infra" }
    }
  ]
}
```

Domínio não pode depender de infra. Se o agente tentar puxar um cliente HTTP pra dentro do use case, o CI barra.⁵

**Pra qualquer stack: Danger.** Danger roda no CI e pode checar qualquer coisa que você defina como regra. Mudou arquivo de migração sem atualizar o changelog? Danger avisa. Criou dependência entre módulos proibidos? Danger barra.

A Böckeler chama esses mecanismos de “sensores computacionais”. São baratos, rápidos e determinísticos. Exatamente o oposto do LLM. E por isso complementam ele tão bem.¹

O Fowler propõe inclusive uma mecânica de feedback loop: toda vez que o sensor pega uma violação, o agente recebe a mensagem de erro e tenta se corrigir. O Fowler chama isso de “positive prompt injection”, uma injeção de contexto que direciona o agente pro caminho certo.¹ O sensor não só barra. Ele ensina.

## Service templates e ambient affordances: arquitetando o ambiente do agente

Agora vou trazer um conceito que pouca gente tá discutindo no Brasil mas que é central: ambient affordances.

O Ned Letcher, da Thoughtworks, usa esse termo pra descrever as propriedades estruturais do ambiente que tornam ele legível, navegável e tratável por agentes. Nas palavras dele: são as propriedades do ambiente em si que o tornam mais “harnessável”.¹

Traduzindo pro português claro: não é só sobre as regras que você escreve. É sobre como o código tá organizado. É sobre a estrutura de pastas. É sobre as convenções de nomenclatura. É sobre os templates que existem.

Service templates são um exemplo poderoso. Quando um time tem um template padronizado pra criar um novo serviço (com estrutura de pastas definida, CI configurado, linter rodando, testes de arquitetura prontos, documentação de domínio incluída), o agente recebe tudo isso de graça. Ele começa num ambiente que já tem as cercas montadas.

A Böckeler e o Fowler deixam claro: times greenfield podem embutir harnessability desde o dia um. As escolhas de tecnologia e arquitetura determinam o quão governável o código vai ser. Já times legados enfrentam o problema mais duro: o harness é mais necessário exatamente onde é mais difícil de construir.¹  
  
Se novo software não precisa nascer cagado!

Se você tá começando um projeto novo hoje e não tá criando service templates com regras arquiteturais embutidas, você tá deixando dinheiro na mesa. Porque todo agente que rodar naquele repo vai trabalhar melhor só por causa do ambiente que você preparou.

Ambient affordances não é sobre prompt. É sobre código. É sobre estrutura. É camada 3 pura.

## Monorepo bem estruturado vs microserviços mal recortados

Hora de falar uma verdade inconveniente.

Monorepo bem estruturado ganha de microserviços mal recortados. Sempre ganhou. E na era dos agentes, ganha com mais folga ainda.

Por quê? Porque num monorepo, o agente tem visão do todo. Ele pode navegar entre módulos, entender dependências, ver os testes de arquitetura, ler os bounded contexts. Tudo tá ali, num lugar só. O contexto é rico e acessível.

Num ecossistema de microserviços mal recortados (aquele onde cada serviço tem 3 endpoints e foi criado porque “microserviço é melhor”), o agente perde o mapa. Cada repo é um universo isolado. O contrato entre serviços tá numa doc desatualizada (ou não tá em doc nenhuma). O agente trabalha num serviço sem saber que a mudança dele vai quebrar o contrato com outros dois. Eu vivo os dois cenários aqui e provavelmente você vai passar por algo semelhante se você trabalha em uma empresa grande.

Não tô dizendo que microserviço é ruim. Tô dizendo que microserviço sem bounded context claro, sem contrato explícito, sem ownership definido, é uma bomba. E com agente, é uma bomba com pavio mais curto.

O DORA 2025 confirma: times trabalhando em arquiteturas frouxamente acopladas com loops rápidos de feedback viram ganhos de produtividade. Times restritos por sistemas fortemente acoplados e processos lentos viram pouco ou nenhum benefício.⁶

O caso da Adidas, citado no DORA, é emblemático: times com arquiteturas frouxamente acopladas e feedback loops rápidos tiveram ganhos de produtividade de 20% a 30%, medidos por aumento em commits, PRs e velocidade de entrega de features. E um aumento de 50% no “Happy Time”, ou seja, mais tempo codando e menos tempo em burocracia.⁶

Oxi, 50% mais tempo feliz. Isso é arquitetura pagando dividendo.

Mas repara: arquitetura frouxamente acoplada. Não microserviço por microserviço. Não repo separado por repo separado. Acoplamento frouxo é decisão de design, não de infra.

Um monorepo com módulos bem recortados, bounded contexts claros, testes de dependência no CI e linguagem ubíqua documentada é frouxamente acoplado. Um ecossistema de 47 microserviços onde todo mundo chama todo mundo via REST sem contrato é fortemente acoplado. Não importa quantos repos você tem.

## O custo concreto de “deixa o agente escolher onde colocar”

Vou te contar o que um mentorado meu me trouxe esses dias. Dois times. Mesma empresa. Mesma feature: implementar um sistema de notificações por e-mail atrelado a eventos de mudança de status de contrato.

![](https://substackcdn.com/image/fetch/$s_!rdXF!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F56741ec8-27a3-48ed-930f-dfff6e460e3e_1609x1115.png)

**Time A: arquitetura explícita.** Monorepo com módulos separados por bounded context: contratos, notificações, comunicações. Cada módulo com sua pasta domain, application, infra. ArchUnit rodando no CI. Linguagem ubíqua documentada num glossário no root do repo. O agente recebeu a task, navegou a estrutura, criou o handler de evento dentro do módulo de notificações, usou a interface de comunicação já definida, escreveu testes contra os contratos existentes. PR aberto. CI verde. Code review em 20 minutos. Deploy sem incidente.

**Time B: arquitetura implícita.** Monorepo grande, mesma empresa, mas sem fronteiras explícitas. Pastas organizadas por tipo (controllers, services, repositories, models) em vez de por domínio. Sem teste de dependência. Sem glossário. O agente recebeu a mesma task. Criou o serviço de notificação dentro da pasta services (junto com outros 140 arquivos). Importou diretamente o model de contrato. Importou o client de e-mail direto no service. Criou um acoplamento entre contrato e notificação que antes não existia. Testes passaram porque eram testes unitários mockados que não testavam a fronteira. PR aberto. CI verde. Code review: reviewer olhou a lógica, achou limpa, aprovou. Deploy. Duas semanas depois, time de contratos fez uma refatoração no model. Quebrou o serviço de notificações. Três horas de debug pra achar que o problema era uma importação direta que nunca deveria ter existido.

Mesma feature. Mesma empresa. Mesmos engenheiros. Resultado radicalmente diferente.

A diferença não foi o modelo. Não foi a ferramenta. Foi a arquitetura.

O custo de “deixa o agente escolher onde colocar” não aparece na hora do commit. Aparece duas semanas depois, quando outro time faz uma mudança legítima e descobre que algo quebrou em cascata. Aparece no debug. Na frustração. Na erosão de confiança no agente. Na reunião de post-mortem onde alguém pergunta: “como isso passou no review?”.

E a resposta é sempre a mesma: porque o review checou lógica local, não integridade arquitetural. E sem sensor computacional, integridade arquitetural é invisível.

## O checklist do engenheiro que leva arquitetura a sério na era IA

Se você leu até aqui, quer o pragmático. Aqui vai:

**1\. Materialize suas fronteiras no código.** Não deixe a arquitetura só no diagrama do Miro. Se a fronteira não tá na estrutura de pastas e nos testes de dependência, ela não existe.

**2\. Instale sensores de arquitetura no CI.** ArchUnit pra Java. Dependency-cruiser pra JavaScript/TypeScript. Danger pra qualquer stack. Se o agente violar uma fronteira, o build tem que quebrar. Sem exceção.

**3\. Documente a linguagem ubíqua.** Crie um glossário de domínio e ponha no root do repo. O agente vai ler. O dev novo vai ler. Todo mundo ganha.

**4\. Defina bounded contexts explícitos.** “Esse módulo é de pagamentos. Esse é de contratos. Esse é de notificações.” Simples assim. Se não tá separado, separe.

**5\. Crie service templates.** Quando alguém criar um módulo novo (humano ou agente), ele já deve nascer com as cercas montadas: estrutura de pastas, CI, linter, testes de arquitetura.

**6\. Prefira organização por domínio, não por tipo.** Pasta por domínio (payments/, contracts/, notifications/) é infinitamente mais navegável pra um agente do que pasta por tipo (controllers/, services/, models/). O contexto fica junto. A fronteira fica visível.

**7\. Rode ArchUnit/dependency-cruiser como teste, não como lint.** Teste quebra o build. Lint avisa. Na era dos agentes, aviso não basta. Tem que travar.

**8\. Faça a arquitetura chata.** Previsível. Explícita. Sem surpresas. Sem atalhos. Sem “a gente arruma depois”. O agente não arruma. Ele acumula.

![](https://substackcdn.com/image/fetch/$s_!7o_w!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd7ebbe2a-2fa6-4004-a78f-c7db6688c9a8_1369x1016.png)

## Fechando o devaneio

Raquel, depois do incidente, fez uma coisa que mudou o jogo do time dela. Passou uma sprint inteira, junto com o tech lead, fazendo só uma coisa: materializar a arquitetura. Separaram os módulos por bounded context. Escreveram testes de dependência com ArchUnit. Documentaram a linguagem ubíqua num glossário no root do repo. Configuraram o CI pra barrar qualquer violação de fronteira.

Na sprint seguinte, o agente tentou fazer exatamente o mesmo tipo de atalho que tinha causado o incidente. A diferença é que dessa vez o CI explodiu vermelho. O agente recebeu a mensagem de erro, corrigiu a dependência, encontrou o caminho certo, e entregou o código respeitando as fronteiras.

Raquel não ficou mais lenta. Ficou mais segura. E o time parou de ter aquela sensação de “funciona, mas sei lá o que vai quebrar amanhã”.

Esse é o ponto central dessa série. A camada 3, a da engenharia de software clássica, é onde o bom engenheiro se destaca. No artigo anterior, eu mostrei isso com testes, linters, type checking. Nesse, mostrei com arquitetura.

Hexagonal, Clean Architecture, DDD. Coisas que muita gente tratou como overkill por anos. Coisas que os puristas defendiam por princípio e que os pragmáticos descartavam por custo.

Agora o cálculo mudou. O custo de não ter arquitetura explícita subiu pra caralho. Porque antes, quem embaralhava as camadas era o dev desatento. Agora é o dev desatento com um agente que escreve 10x mais código por hora.

A velocidade do LLM sem cerca arquitetural é velocidade pra chegar no lugar errado mais rápido.

A pergunta que fica é a mesma do artigo anterior, só com um foco mais estreito: a arquitetura do seu sistema tá explícita o suficiente pra que um agente respeite as fronteiras sem supervisão humana constante?

Se a resposta for “não”... bom, você já sabe por onde começar.

---

*Esse texto é o segundo da série “As 3 camadas do coding com IA”. O primeiro tratou da visão geral das 3 camadas e de por que a engenharia clássica pesa mais do que a maioria imagina. Esse mergulhou em arquitetura. O próximo vai tratar de outro pilar da camada 3. Prepara o espírito.*

*Tu ja deixou o like?! Meu fiiii me ajude, o seu like pra mim é o pagamento pra todo esse trabalho que eu tenho… cuida… agiliza aí!*

---

Se esse é um conteúdo que você acredita que pode ajudar alguém, clica no botão de compartilhar abaixo!

Agora se você quer mais conteúdos como esse na sua caixa de e-mail logo que saírem, é só assinar a newsletter.

---

### Fontes consultadas

¹ Fowler, M. & Böckeler, B. (2026). *Harness engineering for coding agent users*. martinfowler.com https://martinfowler.com/articles/harness-engineering.html

² Miles, R. (2025). *Domain Driven Agent Design*. Engineering Agents (Substack). https://engineeringagents.substack.com/p/domain-driven-agent-design

³ Schleicher, D. (2026). *How Creating a Ubiquitous Language Ensures AI Builds What You Actually Want*. https://www.danielschleicher.com/software/engineering,/ai,/spec-driven/development/2026/01/04/removing-ambiguity-with-spec-driven-development.html

⁴ ArchUnit. *Unit test your Java architecture*. https://www.archunit.org/

⁵ dependency-cruiser. *Validate and visualize dependencies*. https://github.com/sverweij/dependency-cruiser

⁶ DORA / Google Cloud (2025). *State of AI-Assisted Software Development Report*. https://cloud.google.com/blog/products/ai-machine-learning/announcing-the-2025-dora-report

⁷ Fowler, M. (2025). *Harness Engineering, first thoughts*. martinfowler.com https://martinfowler.com/articles/exploring-gen-ai/harness-engineering-memo.html

**Links complementares:**

- Artigo anterior da série: https://zaratips.substack.com/p/as-3-camadas-do-coding-com-ia-onde
- Evans, E. (2003). *Domain-Driven Design: Tackling Complexity in the Heart of Software*. Addison-Wesley.
- Reflectoring.io. *Clean Architecture Boundaries with Spring Boot and ArchUnit*: https://reflectoring.io/java-components-clean-boundaries/
- Xebia. *Taking Frontend Architecture Serious with dependency-cruiser*: https://xebia.com/blog/taking-frontend-architecture-serious-with-dependency-cruiser/