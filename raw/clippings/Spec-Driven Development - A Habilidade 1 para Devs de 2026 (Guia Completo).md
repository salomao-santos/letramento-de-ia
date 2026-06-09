---
title: "Spec-Driven Development: A Habilidade #1 para Devs de 2026 (Guia Completo)"
author: "Waldemar Neto"
source: https://www.youtube.com/watch?v=YFDp-smGYqQ
type: transcript
date: 2025-05-01
language: pt
---

# Spec-Driven Development: A Habilidade #1 para Devs de 2026 (Guia Completo) — Waldemar Neto

## Minuto 0

[00:00] Eu venho usando agentes diariamente no meu dia a dia há muito tempo, Cloud Code, Cursor, Copilot e cheguei numa conclusão que a maioria das pessoas ignora. O modelo, mesmo que os atuais sejam muito bons, não é o suficiente. O que separa um resultado mais ou menos de tu ter um sistema completo e funcional é o contexto que tu dá pro agente. E é aí que entra Spec Driven Development, que é um padrão para desenvolver otimizando o contexto para ter os melhores resultados.

[00:22] Aqui nesse vídeo tu vai aprender como aplicar isso em qualquer code agent para desenvolver com escala, segurança e economizar tokens e evitar retrabalho, que é o que a gente mais quer. Então o que que a maioria das pessoas fazem e se frustram com a IA? Elas pegam uma demanda, por exemplo, aqui eu tenho uma demanda de implementar recomendações no sistema de streaming. Tem tudo aqui a necessidade do negócio — os usuários do sistema de streaming fake, o FakeFlix, não têm recomendação, não sentem que tem uma experiência pensada neles e a gente tem que implementar o sistema de recomendações.

## Minuto 1

[01:01] É uma funcionalidade que vai impactar todo o sistema, toca em vários módulos. E o que as pessoas vão fazer? Ou elas vão tentar quebrar isso em partes menores e aí perdem o contexto entre uma coisa e a outra, ou vão tentar rodar direto a implementação ou gerar um plano a partir de um PRD grande, que tem várias expectativas. Se eu disser "gera um plano a partir desse PRD para mim para implementar", vou ter um plano. O plano não é longo, não é feito para ser longo. A funcionalidade de plano que as ferramentas têm hoje não é feita para ser longa, é feita para fazer uma tarefa bem feita.

[01:36] Mas quando a gente vai fazer um projeto grande, precisa paralelizar tarefa, saber qual tarefa vem primeiro, qual pode ser feita junto com outra, quais dependem de quais. Tudo isso a gente precisa para fazer uma funcionalidade grande. Ao mesmo tempo, usando Spec Driven Development, eu consigo escalar muito mais. Por exemplo, posso criar uma spec que fala da minha feature de recomendações e tem um breakdown de tasks, com qual task vem antes, qual vem depois, a ordem das tasks, as que podem ser paralelizadas.

## Minuto 2

[02:04] Tudo isso eu vou mostrar na prática, mas antes a gente tem que entender como funciona o contexto na LLM pra entender porque Spec Driven Development cresceu tanto e é tão importante. Quando a gente olha para uma janela de contexto, hoje em dia temos janelas de 1 milhão de tokens, mas eu não sugiro vocês usarem elas. Sugiro sempre tentar deixar dentro de 200.000 tokens. Quanto maior a janela, mais chance de alucinar tem.

[02:29] Quando tu começa a usar a IA, o teu agente tem uma janela limpa, ele não sabe de nada. E aí vai entrando coisas: entra o teu prompt, entram os arquivos necessários que ele buscou, entram os agents.md e as rules, entram os MCPs (só os MCPs necessários pro que tu tá fazendo) e as skills necessárias pro que tu vai fazer. Então a janela de contexto tem um tamanho limitado. Quanto maior, mais chance de alucinar. A primeira premissa é otimizar a janela de contexto.

## Minuto 3

[03:01] Mas como que eu faço uma funcionalidade tipo recomendações, onde eu mudei 90 arquivos e mesmo assim não estourei a janela de contexto? Minha janela ficou em 50.000 tokens. Como é possível? Implementando outra coisa que a gente chama de RPI — Research, Plan, Implement. Quando eu tava pensando na funcionalidade, na fase de research, abri um agente para pesquisar. Ele abre uma janela de contexto grande, passa pelo codebase para responder as perguntas. Bate em arquivos relevantes, usa as skills que precisa, busca externo com MCP ou bate no website. Tudo isso na fase de research — estamos descobrindo o que precisa fazer.

[03:40] Depois que estamos mais certos do que tem que fazer, se dermos um prompt a partir daqui para implementar algo, essa janela já tá poluída e vai tender a crescer mais. Não dá pra fazer uma mudança de 90 arquivos a partir de uma janela dessa. E também não queremos gastar tokens — quanto mais prompt, mais tokens gasto.

## Minuto 4

[04:04] O que fazemos a partir daqui? Terminamos a fase de research, salvamos tudo que aprendemos em arquivos Markdown. Assim podemos pegar esses arquivos que já têm todo o resultado da pesquisa e começar a desenvolver em cima deles. Não precisamos gastar mais tokens pesquisando no futuro. Então research — abrimos um leque, fazemos pesquisa — e depois vamos pra fase de plan, que é a fase de planejamento, onde salvamos as coisas.

[04:29] A fase de plano no Spec Driven é onde criamos a spec e o design (se precisar). Podemos também usar o próprio Spec Driven para fazer uma fase de research. É bem comum. A lógica é: primeiro tu abre bastante, depois salva em markdowns para no futuro só reusar esses markdowns durante a implementação. No momento que tu planeja e separa o trabalho em partes, vem a parte de implementar, onde tu pega as tasks que separou durante o planejamento e implementa.

## Minuto 5

[05:03] Como tu tem uma spec e um design muito claros, tu não precisa fazer a fase de research de novo. Já tá tudo definido lá, o agente sempre pode voltar nele. Assim tu economiza tokens pro futuro. E uma pausa rápida — no dia 16 e 17 de maio vai ter a segunda edição do workshop Desenvolvimento Assistido por IA Avançado, onde a gente vai falar de fundamentos de context engineering, spec driven e desenvolvimento autônomo com agentes.

[05:28] E como funciona Spec Driven Development? Vou mostrar a teoria e a prática. O que vou mostrar aqui como base é uma skill que vou deixar disponível para vocês — a TLC Spec Driven. Ela é baseada nos melhores padrões de Spec Driven Development, mas é extremamente flexível. Outro bem conhecido é o Spec Kit do GitHub. Eu não gosto muito dele porque é muito engessado, mas os princípios são os mesmos.

## Minuto 6

[05:50] Quais são os passos? Tem o passo de especificar, ou seja, capturar o que estamos fazendo — esse primeiro é sempre obrigatório. Nele criamos uma spec, que é o que vamos usar como base para depois quebrar o design e as tasks. O que tem na spec? Ela explica o problema, explica o que queremos fazer, qual é a meta (reduzir tempo de play, crescer número de plays), explica o que está fora de escopo, explica as user stories (o que queremos fazer, qual problema do usuário resolve).

[06:23] Isso é importante porque fica como referência para a IA quando ela tá implementando. A spec é quebrada em: problema, goals, o que não tá em escopo, user stories — isso é o contexto geral. Depois vem uma fase opcional de design. Por que o design é importante? Num projeto grande com ~40 tasks, se o design ficar na task, ele vai ficar repetido. Num projeto grande, os designs e diagramas ficam em outro lugar, onde tu pode sempre voltar e referenciar, não importa a task.

## Minuto 7

[07:00] O design fica com decisões importantes do projeto: diagrama de arquitetura da solução, o que vai ser reusado, quais vão ser no alto nível os componentes que vamos precisar, as decisões importantes ficam nesse arquivo. Vocês não precisam criar manual — a própria skill cria. É só para entenderem os passos.

[07:21] Depois vêm as tasks. No momento que tu tem uma spec e um design, tu pode quebrar em tasks. Cada tarefa é entregável. A maneira que ele quebra as tarefas é para ser o mais otimizado possível, pra conseguirmos tomar boas decisões do que pode ser rodado em paralelo, o que não pode, para otimizar a velocidade de entrega e também otimizar o contexto.

[07:44] Se olharmos as tasks, ele quebrou a partir do design o que pode ser sequencial (task 0, task 1 — todas sequenciais). Depois a parte de persistência pode ter várias que podem ser feitas em paralelo. Ele desenhou toda a estrutura de como esse projeto pode ser feito.

## Minuto 8

[08:01] E aqui tem o breakdown de cada task. O que é importante ter numa task? Dizer o que vai ser feito, onde vai ser feito, o que vai ser reusado e o que é pré-requisito de outras tasks. E tem uma definition of done. Por que isso é importante? É que nem um plano. Tem todo o contexto que a IA precisa para escrever esse bloco de código. Ela não precisa fazer uma nova pesquisa quando pega essa task. Pega a task, a task diz tudo que ela tem que fazer, ela só vai lá e executa.

[08:28] Isso faz o quê? Quase elimina a chance de dar erro ou dela fazer algo inesperado, porque ela tem uma coisa muito clara e também tem uma spec para se basear e dá um escopo pequeno. Assim o agente pode tomar a decisão: posso fazer mais de uma task ao mesmo tempo, tenho muitas tasks, ou essa task tá muito grande — ele pode decidir o que fazer. Esse tamanho de task é muito bom porque é muito assertivo.

[08:55] Depois de ter as tasks, vem a fase de executar. Essa fase é muito importante. Hoje em dia temos subagents genéricos, o que nos permite escalar muito e fazer implementações gigantescas sem explodir o contexto.

## Minuto 9

[09:08] Vou mostrar na prática. Quando executei esse projeto para implementar, vocês podem ver que eu dei no prompt: "Use sub agents o máximo possível, não precisa, a maioria das ferramentas novas é inteligente." Mas aqui, em vez de fazer isso na janela de contexto principal, ele abriu sub agents para fazer uma pesquisa. Depois começou a usar subagents para implementar, porque olhou nas tasks o que pode ser implementado em paralelo. Aqui, por exemplo, usou quatro subagents em paralelo para fazer a implementação. Cada um fazendo algumas tasks em paralelo.

[09:43] Isso nos permite otimizar contexto, ter menos chance de erro porque cada agente faz uma coisa específica, e nos permite escalar e fazer uma grande mudança. E tem uma coisa muito importante: quando fazemos uma spec, mais coisas são criadas. Temos um projeto que é a definição de alto nível do projeto como um todo, que tem um resumo dele.

## Minuto 10

[10:04] E tem uma coisa que eu gosto muito, que é o estado. O estado vai guardando decisões importantes que o agente criou durante a implementação. Isso é importante porque podemos simplesmente abrir outra janela, começar o projeto de onde estava, dizer "continua o projeto tal", ele vai funcionar. Posso commitar as specs e seguir o resto do projeto depois. Posso separar em vários pull requests. O estado garante essa continuidade e também guarda decisões importantes que o agente tomou pra gente entender por que ele fez.

[10:40] E como eu uso na prática? Posso simplesmente dizer "me ajuda a especificar o novo projeto". Assim a Skill vai te fazer perguntas até chegar em algo, ou melhor, tu dá um contexto. No caso, como eu tinha um PRD, dei um PRD como base e ela vai ajudar a transformar esse PRD num projeto. Aqui tá me perguntando o que vai ser construído, qual o problema que resolve.

## Minuto 11

[11:03] Se eu der um contexto, ele vai criar tudo que dá para ser criado a partir dali. Se algo não tiver claro, ele vai perguntar. Nesse caso, quando fiz esse projeto, mandei: "Esse é o novo projeto que vou começar, tem o PRD, já fiz uma POC e o recommendations vai ser um novo módulo no sistema. Use a spec driven para planejar o projeto." Com isso, ele criou a spec, criou o design, criou as tasks e depois foi só partir para a próxima janela e ir pra implementação.

[11:32] Por que abri em outra janela? Numa janela fiz a pesquisa, em outra janela limpa de contexto comecei só para implementação. Isso é muito importante.

## Minuto 12

[11:44] E para fechar, como usar essa skill? Essa skill foi criada pela Tech Leads Clube, principalmente pelo Felipe Rodrigues, nosso grupo de pesquisa de IA, e ela é muito boa. É só vir no link que vou deixar. Tem como instalar ela. Instalem ela global — qualquer projeto que eu dou o prompt, ele sai usando. Ela tem toda essa estrutura.

[12:01] Outra coisa muito importante: ela é flexível. Tu nem sempre vai precisar de muita coisa. Às vezes tu só quer uma spec e as tasks. Design é opcional. Tu pode simplesmente dizer "tô planejando um projeto pequeno, cria as tasks" — ele vai pular a parte de design. Para projetos grandes, sugiro usar todas as fases, mas com isso vocês vão conseguir desenvolver em escala, seguindo esse processo.
