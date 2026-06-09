---
title: "Rules, Skills, MCPs e Subagents - DOMINE os principais conceitos de IA para ganhar PRODUTIVIDADE"
author: "Waldemar Neto"
source: "https://www.youtube.com/watch?v=omkEi4GTCj8"
type: transcript
date: 2025-02-07
language: pt
---

# Rules, Skills, MCPs e Subagents - DOMINE os principais conceitos de IA para ganhar PRODUTIVIDADE — Waldemar Neto

## Introdução

Skills, rules, sub agents, MCPs, tudo isso em uma aula completa, onde tu vai aprender a usar os principais conceitos para ganhar produtividade com IA com segurança. Essa é uma aula da Tech Leads Clube que eu editei especificamente pro YouTube para ser direto ao ponto. Além disso, tem um presente especial que é uma biblioteca de skills que a gente fez com skills curadas e a gente vai mostrar umas skills bem legais que já estão disponíveis lá.

Qual que é a estrutura da live aqui? Então vamos passar um pouco mais pro contexto, que é isso que eu tô falando. Vou mostrar um fluxo real rapidinho. A partir desse fluxo real, a gente vai entender o que que mudou no fluxo, nos fluxos agênticos nos últimos tempos e o que usar — agents.md, rules, skills. E lá no final a gente vai falar se que é o fim dos custom agents, o que que tá substituindo eles e depois eu vou deixar também ali meio que uma previsão do futuro do que que eu acho que vai acontecer.

## Fluxo Real — Demonstração

O que que eu quero começar aqui com fluxo pra gente refletir é o seguinte. Então, eu tenho um board do Jira e eu tenho um bug aqui no board do Jira, né? Então, esse aqui um JWT token válido quando o usuário faz login com e-mail uppercase, tá? Isso aqui é só um exemplo de uma task, não se preocupem, só um exemplo de um fluxo real.

Eu vou pegar aquela task de lá, eu vou dizer assim: "Ah, crie um plano para fixar o bug KAN." E aqui eu tenho um fluxo que é bem moderno, assim, a gente vai entender como ele funciona e vai entender tudo que tá envolvendo ele pra gente conseguir fazer algo desse tipo aqui.

Primeiro ele foi lá, pegou a task, tá certo? Ele viu que, e tu vê que ele tá tudo interpretando, agora conseguiu pegar a task, beleza. E aqui ele pegou a task lá do Jira e ele abriu aqui embaixo vários sub agents para começar a explorar como a implementação vai ser para criar um plano.

Então aqui, já aconteceu muita coisa que quem vem seguindo IA há uns 3 meses atrás, não era assim. A gente tinha muito mais trabalho manual para fazer só isso aqui, só para criar esse plano aqui. E vocês forem ver meu contexto tá baixo também, que é uma coisa importante.

Então, o que que envolveu aqui para ele fazer essa exploração para criar um plano de implementação? Para mim envolveu chamar uma skill, que a gente vai explicar o que que é. Então, aqui tem uma skill, eu tenho uma skill que sabe buscar tasks do Jira no meu projeto. Então, eu só dei ali criar um plano para fixar o bug. Ele sabe, bug, task tá no Jira. Foi lá, buscou. Beleza? Segundo, ele sabe que a skill sabe que para buscar task do Jira eu tenho que usar o MCP. E uma coisa que mudou muito na IA nos últimos tempos foi a gente começar a usar mais sub agents para manter o contexto do agente principal menor.

Então quando tem que buscar arquivos, sumarizar, pegar, tu abre uma pesquisa grande, depois tu resume e dá resposta pro agente principal. Isso acontece aqui — para quem usa Claude Code é uma task, né? Ele faz uma task bem similar a isso, mas ele falou lá, fez um processo e trouxe de volta. E aqui tem uma análise completa que virou um plano para mim implementar. Então só aqui tem vários conceitos pra gente entender.

## Contexto Histórico — Evolução dos Fluxos Agênticos

A gente começou aqui, né, a parte mais fundamental de Transformers, não vou entrar muito nisso, mas depois a gente foi pro ChatGPT3 que saiu, ninguém deu muita bola. Aí a gente começou aqui mais ou menos em 2023, 2022 para 2023, a gente começou a usar IA muito pesado mesmo. Então a gente começou janelas de contexto maior. Então o Claude começou ali chegar a 200.000 tokens. A gente começou a ter o GPT4 ali com 128.000 tokens e tal. A gente começou a usar para coisas maiores, para code base, e comecei a ter um grande retorno ali, mais ou menos por 2023.

2023 para 2024 entrou principalmente MCPs. Então Anthropic, que é a empresa do Claude, criou um protocolo que todo mundo adotou. E MCP serve para quê? MCP serve para buscar, principalmente buscar dados externos. Então tu precisa de um contexto externo. Ali, por exemplo, dei um prompt e ele buscou uma task do Jira. Essa task é como uma chamada de API, né? Eu preciso de um contexto que tá fora. Vai lá, busca e traz esse contexto para mim usar dentro do meu prompt local, ali na minha janela de contexto local. E isso abriu muitos use cases.

### O Problema do Contexto Inflado

Só que o que aconteceu nessa época aqui, 2024, no início de 2024, a gente começou a botar muita coisa no contexto. A gente começou a usar para código, a gente começava a botar IA num code base e aí a gente dava o máximo de documentação possível, carregava quase todo o code base e aí plugava o MCP. E o que que acontece quando o contexto infla? Você tem uma janela de contexto muito grande.

Isso é um teste fácil de vocês fazerem. Até numa janela, vocês abre uma janela com ChatGPT, começa a conversar com ele e começa a conversar de vários assuntos ao mesmo tempo na mesma janela, vocês vão ver que as respostas que ele dá começam a perder o sentido, porque ele tem muita coisa diferente no contexto e o contexto tá muito grande.

Então a gente foi aprendendo que o mais importante para a IA não alucinar é a gente ter um contexto muito claro e focado com uma responsabilidade só. E hoje em dia a gente fala que o ideal numa janela do contexto de uns 200.000 tokens é tu ter no máximo uns 40% da janela ocupada. A partir disso, tu já vai começar a ter respostas que não são muito precisas.

E sempre usar planos, né? O plano também veio mais ou menos ali no meio de 2024, começou a ficar bem comum em todas as ferramentas, porque ele dá esse passo a passo pro agente saber como implementar. Então, uma janela de contexto menor e um passo a passo claro normalmente dá um sucesso muito grande de resposta nos agentes.

### Progressive Disclosure

2025 foi um ano de estruturar cada vez mais o contexto — como as ferramentas são carregadas, como o contexto é carregado para ocupar menos espaço na janela de contexto para alucinar menos. Aí entrou esse conceito de progressive disclosure, que é a IA descobrindo, o agente descobrindo automaticamente as coisas. Ele carregando. Então, se tu tem agora skills, ele carrega automaticamente. Antes MCPs, por exemplo, tu definia vários MCPs e tu imagina que um MCP é como se fosse uma definição numa API. E essas definições ficavam tudo na memória do agente quando ele iniciava.

Hoje em dia tem o search tool lá que começou acho que com Anthropic que eles implementaram primeiro, que o próprio agente sabe, "agora eu vou precisar do MCP tal", ele vai lá e carrega. Então, a janela de contexto hoje em dia tá muito mais otimizada e cada vez mais a gente vem trabalhando para isso.

## Arquitetura Antes vs Agora

### Como funcionava antes (2024)

Antes ali por 2024 a gente tinha todas as coisas — as instruções, os MCPs, as regras do projeto, a documentação do projeto, os workflows — tudo junto, tudo carregava ao mesmo tempo. E aí tu tinha um prompt gigante, a tua janela de contexto explodia, as pessoas reclamavam da IA: "IA tá alucinando, output não faz sentido, tô gastando muito token."

Imagina, tu pega os modelos da Claude, tu gasta muito tokens, tu manda um contexto gigante e obviamente ficou um problema claro que a indústria começou a tentar resolver.

### Economia de contexto

A gente é cobrado na entrada e na saída. Então assim, tem um gasto ali da empresa. Então quanto mais coisa você mandar para ela, mais o seu limite vai embora mais rápido. Não tem almoço grátis.

### Estrutura de hoje

A gente tem a estrutura de hoje de como a gente estrutura um contexto. E assim as ferramentas cada vez mais vão automatizando isso. A gente tem que entender o que fazer e quando, mas as ferramentas cada vez mais vão entregando isso para nós de forma automática.

Eu tô usando essas coisas que se aplicam pro Cursor, se aplicam pro Claude Code, se aplicam pro Copilot. Skills é padrão de indústria, MCP é padrão de indústria, agents.md padrão de indústria.

## Rules

O que que são rules? São basicamente guidelines estáticos que tu dá pro agente. Então, a gente inicia e ele carrega essas coisas. Que que a gente bota em rules? Estilo de código, convenção do projeto, estrutura.

Aqui eu tenho meu architecture rules. Que que ele diz? Ele não é grande. E o que que ele tem? Ele explica a estrutura de alto nível do meu projeto. E ele explica também aonde buscar outras documentações. "Se tu precisar de entendimento geral da arquitetura, busca esse aqui." Então ele carrega só o básico, tem uma estrutura de alto nível e o resto ele carrega se ele precisar.

Isso aqui são rules do Cursor. O que que aconteceu? O Cursor tem essas rules desde o início. Foi uma coisa que fez ele se destacar bastante porque não tinha um padrão de agents.md na época. Hoje em dia tem. Então a indústria foi lá, todo mundo falou: "Vamos botar um padrão para isso". Então se quiser ter a mesma coisa que eu tenho aqui nesse Markdown, pode só copiar esse arquivo e criar um agents.md no root. E o agente vai carregar ele por padrão também, que vai ter um efeito bem similar à minha rule aqui.

E aqui essa minha rule, ela sempre aplica, ou seja, sempre que a gente inicia ele aplica. Eu posso ter rules também que carregam sob demanda. Posso dizer que ele "always apply false" e aí ele vai carregar só quando ele precisar.

### agents.md

O agents.md é um basicamente um markdown naquela mesma estrutura que o agente pega e carrega. Ele não deve ser muito longo, no máximo umas 200 linhas e só a estrutura e onde carregar o resto das coisas. Esse aqui é um projeto X. Essa aqui é arquitetura de alto nível. Se tu quiser mais informação da arquitetura, vai no meu doc arquitetura. Se tu precisar de padrão de implementação pro banco de dados, vai no meu padrão de implementação pro banco de dados. Ele vai carregando sob demanda, o que ele precisa. Assim a janela de contexto vai se mantendo baixa.

## Skills

### O que são Skills

Skills são basicamente uma funcionalidade portável. Então aqui no meu caso, se eu vier aqui na minha aplicação, em cursor skills, eu tenho minhas skills. Olha o que que são as skills que eu criei pro meu projeto:

- **Jira assistant** — se eu vou pegar uma task do Jira toda hora, eu criei uma skill que é o Jira assistant.
- **Confluence** — buscar/criar uma página no Confluence
- **Criar testes end to end** — não preciso estar escrevendo toda vez como fazer

### Por que Skill em vez de MCP direto?

"Por que que tem uma skill sendo que já tem o MCP da Atlassian?" Porque é o seguinte: pensa assim, se toda vez que eu for batendo naquela API no meu código, tiver que escrever toda a requisição, botar token, fazer toda aquela coisa ali, eu vou levar tempo. O que que a gente faz? A gente abstrai a parte de chamada de API numa classe. A skill é a mesma coisa.

A skill sabe usar o MCP. O MCP da Atlassian é meio lento, todo MCP é meio lento. Então, por exemplo, o que que a skill faz? Ela usa o MCP da Atlassian para fazer as coisas e ela já sabe qual é o meu projeto lá no Jira. Tá configurado aqui. Por isso que eu dou um prompt "fixar um bug". Ele já sabe qual a instância do Jira, ele sabe onde tá o board e traz. Se eu não tivesse essa skill, toda vez que eu falasse isso aqui, ia ter que falar: "fixar o bug na URL techlads.atlassian.net, cloud digital, board KAN" — só isso aí já ia gastar tempo.

Então quando ele chama essa skill, ele não tem que pensar, tá tudo certo aqui. E dessa maneira a gente consegue otimizar um monte de fluxo.

### Skills carregam sob demanda

Eu não preciso dizer "usa a skill", não. O próprio agente sabe, ele sabe o que carregar sob demanda e usar. A gente só tem que criar esse skill.md. E às vezes criar esse skill.md envolve quase nada de trabalho manual. Tu vai, tu faz uma coisa uma vez manualmente, diz: "a partir do que a gente conversou nesse chat, cria uma skill" e aí o próprio agente vai lá e cria uma skill para ti.

### Diferença entre MCP e Skill

MCP puro sem skill: toda vez você precisa instruir URL, token, autenticação. O MCP pelo menos faz um OAuth, então é transparente. Eles criaram um protocolo que todo mundo segue. Tu configurou ele, o teu agente já sabe achar ele automático, zero esforço depois disso.

Quando você usa um MCP, você não usa só para busca, você pode usar para busca, para inserção, para atualização. Então, um uso que eu tô costumando fazer: pegar a task do Jira, mas também colocar comentários. Criei uso MCP do GitHub, vai lá, cria o PR, mas adiciona lá na task o comentário, o PR foi criado. Então, você não precisou fazer um mapeamento de outras APIs.

## Sub Agents — Como Eram

### O agente customizado do Felipe

O Felipe mostrou um sub agent antigo: um sub agent criado baseado em toda a documentação do repositório. Várias instruções de como são os padrões no repositório, onde estão cada coisa, como criar componentes no React, como fazer comunicação com endpoints do backend. Tinha MCPs que ele deveria usar antes de mexer em algo, como consultar documentação de libs.

Toda vez que você começava uma conversa já ia metade embora do contexto só com aquilo ali. Então às vezes não sobrava nem contexto para tarefa. Quem usa o Claude no plano mais barato, carregava isso tudo, falava "oi" e já parecia que 5 horas sem poder usar porque o limite era levado embora.

### Por que as pessoas criavam sub agents

Até setembro do ano passado, era bem comum esses casos de uso. A indústria começou a ver que as pessoas estão criando sub agents não só pela coisa de rodar num processo separado, mas para ter algo especializado: criar PDF, criar teste, fazer release.

Então, tu tinha separação em duas coisas: o sub agent era responsável por rodar algo no background E por uma responsabilidade específica.

## A Mudança: Skills Substituem Sub Agents para Capabilities

A indústria começou a ver: "as pessoas estão usando sub agents para capacidade, então a gente pode ter uma skill que roda no contexto que ela tá e o sub agent ser uma coisa separada."

Até 2024, final de 2024, início de 2025, a gente vinha criando sub agents para habilidades. Ah, o agente que cria um PDF, o agente que faz o debug, o agente que cria testes. E o que que eles descobriram? Se a gente fizer um agente genérico que inicia um processo novo e aí ele tem várias habilidades a partir dali, então a pessoa não precisa definir um agente mais, ela define só as habilidades e o agente ele é genérico.

### Sub Agents Genéricos (estado atual)

Sub agents genéricos — o Cursor começou a implementar agora, demorou um pouco, mas o Claude Code já tem um bom tempo. A ideia é que eles são de propósito genérico mesmo. Pode dizer para eles: "explora tal coisa, busca tal coisa em paralelo", ele vai lá, vai iniciar o processo separado e vai fazer essa análise e vai trazer pro agente principal.

Isso é muito poderoso. Por que? Porque agora as skills são a capacidade. Então um agente desses pode chamar várias skills e ele roda em outro processo. A skill roda no processo que ela tá, ou seja, ela roda no contexto do agente que ela tá. Ela não tem nenhuma otimização do contexto, mas o sub agent tem.

Então tu pode dizer: "Olha, analisa minha arquitetura." E eu consigo dizer para ele fazer um processo em paralelo. Eu não tenho nenhum agente configurado, mas eu tenho skills. Os agentes podem ou não podem usar essas skills, fica por eles, mas eu consigo fazer várias coisas em paralelo sem interferir em nada no meu contexto principal.

E essa aqui é a mudança mais interessante dos últimos tempos na IA. A gente consegue fazer várias coisas em paralelo, vários sub agents em paralelo sem afetar o contexto principal.

## Como o Felipe Migrou: De Sub Agent para Skills

Aquele sub agent grande virou tudo isso aqui: core standard, create component, form, integrate API. Porque antes quando chamava o sub agent, ele vinha com contexto de como arrumar teste, como implementar formulário, como criar componente. Agora não, ele vai lá no core standards, ele vai entender onde tá o arquivo de configuração do Jest ou do Vitest, onde estão os mocks. Ele não precisa saber como implementar o formulário para aquela conversa ali, isso é totalmente irrelevante.

Esse arquivo ficou com 66 linhas. E toda vez que você abre uma conversa que tem as skills dentro da pasta correta, ele carrega só o front matter. Quando você manda um "oi" lá, ele já manda isso. Então ele sabe que tem. E como ele sabe quando usar? Na description: "use when task mentions schemas validation field arrays disabled states". Então ele já chama automático.

### Dá para fazer skill de qualquer coisa

Dá para fazer skill de qualquer coisa mesmo. Eu uso skills no Claude web para fazer apresentação de slide, criar PDF, criar RFC, criar design doc.

## Checklist Final — Resumo de Conceitos

### agents.md / Rules (estático)
- Definir regras da arquitetura, da estrutura e padrões que tu quer que sempre siga
- Estrutura do código, desenho da arquitetura, convenções, documentação
- Onde achar mais documentação
- "Se precisa de entendimento, é coisa estática: agents.md e rules"

### Skills (capabilities)
- Funcionalidade portável, habilidade
- Fazer análise de arquitetura, avaliar módulos, criar teste end to end, criar um módulo
- Coisas que ele sempre vai fazer e vão ser igual → vira skill
- Portáveis — pode mandar para outro projeto, pode usar em qualquer IDE

### MCPs (conexão externa)
- Pegar coisas externas, conectar com coisas externas
- Interface para falar com o mundo externo e trazer o contexto para dentro

### Diferença-chave
- Skills vieram para resolver o problema das pessoas usarem sub agents para fazer coisas que seriam habilidades
- Sub agent é necessário quando tu quer criar um processo diferente, para limitar o contexto do processo principal
- Encapsular uma funcionalidade → skill. Isolar contexto → sub agent genérico

## O Fim dos Custom Agents

Hoje em dia a ideia que todo mundo tá passando (pessoal do Cursor, da Anthropic, do Claude Code) é: foquem mais em ter skills, que a parte de agente a gente vai resolver. Então as ferramentas cada vez mais vão ser inteligentes de saber o que delegar para um agente. Tu falar "paralelo", tu falar "analyze", tu falar "show me" — todo esse tipo de coisa, ele sabe criar um agente novo.

E esse agente é inteligente de receber parte do contexto, de buscar as skills, de trazer de volta o mínimo possível para te manter a tua janela de contexto aqui sempre otimizada.

## Presente: Biblioteca de Skills Curadas

A gente criou uma lib com skills curadas e pré-selecionadas pelo pessoal do Tech Leads Clube. O repositório é aberto, qualquer pessoa pode colaborar.

### Problema que resolve

Tem um monte de marketplaces de skills, mas quando você entra lá, vê 5000 skills. Muitas não seguem boas práticas — a galera praticamente só pegou o agents.md e converteu para skill. Você entra, ele tem 2000-3000 linhas. E quando a Anthropic deixa claro que tem que ter no máximo 500 linhas para ficar balanceado.

### Como funciona

A lib já instala tudo nos lugares corretos. Você seleciona a skill, ela já detecta quais IDEs você tem na máquina. Você pode selecionar qual quer instalar. Ele pergunta se quer um link simbólico ou copiar. Recomendação: deixar no symlink porque assim toda atualização da lib já atualiza automaticamente.

### Skill de Spec Driven Development

Uma das skills disponíveis é uma simplificação do spec kit do GitHub. Tem instruções de design, de implementação, de especificação, de como criar as tarefas, e de validação. Quando vai criar a tarefa, ele vai te perguntar: "Para essa tarefa, você quer usar algum MCP ou alguma skill em específico?" Você vai desenvolver como se fosse um bate-papo, mas ele já tem ali as instruções de seguir boas práticas.

## Diferença entre Agent e Skill (contribuição do público)

- **Agent** = o chapéu que o agente vai vestir, é o papel que ele vai assumir, a sua personalidade. "Você vai agir como um testador, como um code reviewer."
- **Skill** = instrução para executar alguma tarefa, independente do papel. A skill do Jira pode ser usada por qualquer agent.

## Sobre Gasto de Tokens

A gente gasta um pouco mais de tokens sim usando guidelines, mas ao longo prazo a gente tem uma economia. Num processo de desenvolvimento fim a fim, desde o planejamento até a entrada em operação, no contexto geral você acaba economizando. A partir do momento que você gasta mais planejando, tem seus guidelines, tem seu agent e suas skills bem definidas, focando o agente a fazer estritamente o que você exige com o nível de qualidade que você exige, no decorrer do desenvolvimento você vai gastar menos token — porque é menos token de retrabalho, de bug que tem que corrigir, de código duplicado, alucinações.

Você tá investindo. Gasta um pouco mais no início, mas ao longo do ciclo de desenvolvimento, vai ter economia sim.

## Centralização de Conhecimento em Times

Normalmente empresas começam a centralizar o conhecimento em algum lugar e usam o MCP para pegar esse dado, padrões atualizados. Tem que avaliar: quão frequente isso muda? Se não muda com tanta frequência, daqui a pouco ter um marketplace interno de skills é o que as empresas estão fazendo. Toda vez que alguém atualiza, faz uma release nova da skill, tu vai lá, atualiza o teu local, tu tem acesso à última versão.

Se tu carregar tua IDE com muitos MCPs numa empresa grande com centenas de MCPs, vai ficar lento. Uma skill é melhor nesse caso. Onde que não dá para usar skill: quando tu tem coisas dinâmicas. Algum conteúdo que mude com frequência, que venha do banco de dados — é melhor centralizar e ter o MCP que pega ele sempre atualizado.
