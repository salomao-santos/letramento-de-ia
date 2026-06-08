---
title: "Devs são os novos pilotos de avião (e ninguém tá te preparando pra isso)"
source: "https://zaratips.substack.com/p/devs-sao-os-novos-pilotos-de-aviao"
author:
  - "[[Zarathon \"Zara\" Viana]]"
published: 2026-04-09
created: 2026-06-08
description: "O que a aviação já sabe há 40 anos que a engenharia de software tá descobrindo agora"
tags:
  - "clippings"
---
Em 2009, um Airbus A330 caiu no Atlântico. Voo Air France 447, Rio-Paris. 228 pessoas morreram. O avião estava funcionando perfeitamente. Os motores estavam ligados. Os controles respondiam. O que falhou foram os pilotos.

Quando os sensores de velocidade congelaram e o piloto automático desconectou, três pilotos treinados precisaram assumir o controle manual de uma aeronave que voava há horas no automático. Eles não conseguiram. Em 4 minutos e 23 segundos, um avião perfeitamente funcional foi jogado no oceano por uma tripulação que não entendeu o que estava acontecendo.

Agora me diz: isso te lembra alguma coisa?

Porque pra mim, o que tá acontecendo com desenvolvedores de software em 2026 é assustadoramente parecido. E o mais preocupante é que quase ninguém tá tratando o problema com a seriedade que ele merece.

![](https://substackcdn.com/image/fetch/$s_!FDBP!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8796155d-66c7-4a40-a9dd-66eb8d61ca18_2752x1536.png)

## O autopilot já tá ligado. E você talvez nem tenha percebido

Olha os números: em 2026, 84% dos desenvolvedores já usam ferramentas de IA no dia a dia. Código gerado por IA já representa algo entre 27% e 41% de todo código em produção, dependendo da fonte que você consultar¹². O Stack Overflow Developer Survey de 2025 mostrou que 65% dos devs usam essas ferramentas pelo menos toda semana³.

O Cursor, o Copilot, o Claude Code viraram o autopilot da cabine do desenvolvedor. Você descreve o que quer, a IA gera, você revisa (ou não) e segue em frente. É cômodo. É rápido. É perigoso pra caralho.

E tem um agravante que ninguém tá discutindo com a honestidade necessária: existe um push brutal vindo da alta gestão pra adoção de IA em times de engenharia. CEOs e CTOs estão sob pressão de boards e investidores pra mostrar que estão “usando IA” e “aumentando produtividade”. O Satya Nadella da Microsoft e o Sundar Pichai do Google já saíram dizendo publicamente que cerca de 25% do código das suas empresas é gerado por IA. O Dario Amodei, CEO da Anthropic, chegou a prever que em 6 meses 90% de todo código seria escrito por IA. Isso cria uma corrida onde o objetivo vira “adotar IA o mais rápido possível” e não “adotar IA da forma mais inteligente possível”. É como se a companhia aérea mandasse os pilotos ligarem o autopilot logo depois da decolagem e só desligarem no pouso, sem considerar as condições de voo. A pressão vem de cima, mas quem paga o preço quando dá merda é quem tá na cabine.

Perigoso por quê? Porque a aviação já estudou exatamente esse fenômeno. Há décadas. E as conclusões são perturbadoras.

## As ironias da automação: um paper de 1983 que previu 2026

Em 1983, uma pesquisadora chamada Lisanne Bainbridge publicou um paper chamado “Ironies of Automation” (Ironias da Automação)⁴. Esse trabalho tem mais de 1.800 citações e é considerado um marco na pesquisa de fatores humanos. A tese central dela é brutal na sua simplicidade: ao tirar as partes fáceis do trabalho, a automação torna as partes difíceis ainda mais difíceis.

Relê isso. Devagar.

Ao tirar as partes fáceis, a automação torna as partes difíceis ainda mais difíceis.

É exatamente o que tá acontecendo com dev. O Copilot escreve o CRUD. O Claude Code monta o boilerplate. O Cursor autocompleta a lógica de negócio simples. Massa, você ganha velocidade nas partes fáceis. Mas e quando o sistema dá pau em produção às 3 da manhã? E quando o bug tá numa race condition que a IA gerou sem entender o contexto? E quando a arquitetura que foi “vibecodeada” começa a desmoronar sob carga real?

Aí é a decolagem com turbulência. E se você nunca praticou o voo manual, se lascou.

Bainbridge identificou que quando os operadores são relegados ao papel de “monitores” da automação, três coisas acontecem: eles perdem a prática das habilidades manuais, eles perdem consciência situacional (situational awareness) do que o sistema tá fazendo, e eles não conseguem retomar o controle quando a automação falha. Troque “operadores” por “desenvolvedores” e “sistema automatizado” por “IA” e você tem o retrato exato de 2026.

Mas tem um detalhe que torna a situação dos devs potencialmente pior do que a dos pilotos. E esse ponto é fundamental.

Em toda a história da engenharia de software, quando subimos a camada de abstração, saímos de determinístico para determinístico. Quando migramos de Assembly para C, de C para Java, de Java para frameworks de alto nível, o comportamento do sistema continuava previsível. Dado o mesmo input, você tinha o mesmo output. Sempre. Isso mudava a forma de escrever, mas não mudava a natureza do que estava sendo escrito.

Com IA generativa, quebramos esse contrato. Pela primeira vez, estamos saindo de determinístico para probabilístico. O código que a IA gera não é uma tradução direta da sua intenção. É uma inferência estatística do que provavelmente você quer. Às vezes acerta. Às vezes chega perto. Às vezes gera algo que parece certo mas tem um bug sutil que só vai aparecer em produção sob condições específicas. É como se o autopilot do avião não seguisse regras fixas de aerodinâmica, mas sim fizesse uma estimativa do que provavelmente é o comportamento correto. Imagina voar num avião assim. Pois é. Bem-vindo ao desenvolvimento de software em 2026.

## Os dados que a aviação já tem (e que dev tá ignorando)

A pesquisa em aviação sobre degradação de habilidades com automação é extensa. E os dados são assustadores quando você faz o paralelo com software.

Um estudo comparando desempenho de grupos usando automação vs. controle manual mostrou que o grupo com automação sofreu uma degradação de performance de 61% ao longo do experimento, contra 31% no grupo manual⁵. Pilotos que usam autopilot extensivamente passam até 89% do tempo de voo em sistemas automatizados, e pesquisas mostram que mesmo pilotos experientes com média de 17.844 horas de voo apresentaram enfraquecimento em habilidades de voo manual⁶.

Mas o dado que mais me arrepia é esse: um estudo da METR, publicado em 2025, fez um ensaio controlado randomizado com 16 desenvolvedores experientes em seus próprios repositórios open source. Resultado? Quando usavam ferramentas de IA, os devs levavam 19% mais tempo pra completar as tarefas. A IA os deixou mais lentos⁷. E o pior: antes de começar, esses mesmos devs estimaram que a IA os tornaria 24% mais rápidos. Depois de terminar, ainda acreditavam que tinham sido 20% mais rápidos, mesmo tendo sido mais lentos na prática.

Vixe Maria. Isso tem nome na aviação: automation complacency (complacência por automação). É quando o operador confia tanto no sistema automatizado que para de questionar, para de verificar, para de pensar criticamente. E quando essa confiança excessiva encontra uma falha do sistema, o resultado é catastrófico.

Na aviação, isso causa acidentes. Em software, causa sistemas frágeis, bugs em produção, dívida técnica acumulada e, no longo prazo, profissionais que não sabem mais resolver problemas sem a muleta da IA.

## Horas de voo: a métrica que dev deveria adotar

Na aviação, o conceito de “horas de voo” não é só uma métrica de vaidade. É requisito regulatório. No Brasil, a ANAC (Agência Nacional de Aviação Civil) exige no mínimo 150 horas de voo para a licença de Piloto Comercial. Mas na prática, as companhias aéreas brasileiras exigem muito mais: a LATAM, por exemplo, pede no mínimo 500 horas de voo, e em momentos de alta oferta de pilotos esse número já chegou a 5.000 horas. Para ser comandante de linha aérea, estamos falando de 3.000 a 4.000 horas de voo acumuladas⁸.

E perceba que a formação do piloto no Brasil segue uma progressão clara e regulamentada: primeiro o curso de Piloto Privado com mínimo de 35 horas práticas, depois o Piloto Comercial com mais horas, depois a habilitação IFR (voo por instrumentos), depois horas como co-piloto sob supervisão de um comandante experiente. Ninguém sai do aeroclube e senta na cadeira esquerda de um Airbus A320. Ninguém. O custo dessa formação? Entre R$ 110 mil e R$ 160 mil só até a licença comercial, segundo estimativas do mercado.

Agora olha como funciona em dev: você faz um bootcamp de 6 meses, ou uma faculdade de 4 anos onde muita coisa é teoria, e o mercado espera que você “dê conta” desde o primeiro dia. Não existe um equivalente às horas de voo. Não existe uma progressão regulamentada. E com a IA, a tentação de pular etapas ficou irresistível.

Eu acredito que devs precisam construir suas “horas de voo”. E a boa notícia é que, diferente da aviação, você não precisa de um avião de 100 milhões de dólares pra isso.

## O simulador, o voo solo e o primeiro voo comercial

Aqui é onde a analogia fica mais rica, e onde eu vejo caminhos concretos pra quem tá entrando no mercado agora.

**A faculdade (e os bootcamps) são o simulador de voo.** Você aprende os fundamentos num ambiente controlado, sem consequência real. Ninguém morre se seu código de trabalho da faculdade tiver bug. E tá tudo bem, é pra isso que o simulador existe. O problema é que, com ferramentas de IA, muita gente tá passando pelo simulador sem de fato aprender a pilotar. Tá usando o autopilot até no simulador. Aí quando chega a hora de voar de verdade, não tem repertório nenhum.

**Mas eis o ponto crucial: diferente da aviação, no dev você pode sair do simulador mais cedo e com mais opções.** Um aspirante a piloto precisa de centenas de horas supervisionadas antes de pilotar sozinho. Um dev pode começar a acumular “horas de voo real” muito antes, através de:

**Micro-SaaS e projetos próprios.** Construir um produto pequeno e colocar em produção com usuários reais. Isso é o equivalente ao voo solo. Não tem instrutor do lado. Se der merda, é você que resolve. E é exatamente esse tipo de exposição que constrói o repertório que a IA não te dá.

**Contribuição open source.** Participar de projetos maduros, com code review rigoroso e padrões reais. É como co-pilotar com um capitão experiente. Você vê como decisões são tomadas em contexto real, com trade-offs reais.

**Freelance em projetos pequenos.** Voos curtos, risco relativamente baixo, mas com consequência real. Se o cliente fica insatisfeito, se o sistema cai, o problema é seu.

**Build in public.** Construir aberto, mostrando o processo, recebendo feedback do mercado. É como voar com o rádio aberto pro controle de tráfego: tem gente monitorando, dando feedback, e isso te força a manter um padrão.

**Hackathons com produto real.** Não os hackathons de faz-de-conta onde ninguém usa o resultado. Mas aqueles onde o produto final tem chance de virar algo real. É o voo com simulação de emergência: pressão real, tempo limitado, problemas inesperados.

Cada uma dessas experiências é uma hora de voo no seu log. E nenhuma delas pode ser substituída por 50 prompts no Cursor.

## O piloto moderno: mãos no manche na hora certa

Agora, se você já tá no mercado, trabalhando, o paralelo muda um pouco. Porque o piloto moderno de linha aérea não voa no manual 100% do tempo. Na real, ele usa automação na maior parte do voo. E isso é correto. Eficiente. Seguro.

Mas existem dois momentos em que o piloto obrigatoriamente assume o controle manual: a decolagem e o pouso. Porque são as fases de maior risco, maior complexidade e menor margem de erro.

O dev de 2026 precisa pensar igual.

Deixa a IA gerar o boilerplate? Beleza. Deixa o Copilot autocompletar aquele CRUD básico? Tranquilo. Mas a definição da arquitetura? É voo manual. O design de um sistema distribuído? Mãos no manche. A investigação de um bug complexo em produção? É você que pousa esse avião. A decisão de trade-off entre consistência e disponibilidade? Não tem prompt que resolva.

E deixa eu ser preciso aqui: eu não tô dizendo que você não pode usar IA nessas fases críticas. Pode. Assim como o piloto tem instrumentos de apoio durante o pouso. Mas a IA nessas horas é um acessório, um instrumento a mais no painel. Quem tá no comando é você. Quem toma a decisão é você. Quem responde quando dá errado é você. Se você tratar a IA como o piloto e você como o passageiro nessas fases, a analogia do AF447 deixa de ser metáfora e vira profecia.

E tem um terceiro momento crucial: quando as coisas dão errado. Quando o autopilot desconecta. Na aviação, chamam de “automation surprise” (surpresa de automação). É quando o sistema automatizado faz algo inesperado, ou para de funcionar, e o operador precisa entender rapidamente o que tá acontecendo e assumir o controle.

Em dev, isso é o incidente em produção. O deploy que quebrou. A integração que parou de responder. A IA não vai salvar você nessa hora. Na verdade, se você desenvolveu complacência com automação, a IA pode até atrapalhar, porque você vai perder tempo tentando fazer ela resolver algo que exige entendimento profundo do sistema.

## O elefante na sala: quem forma os novos pilotos?

Agora chegamos na parte que mais me preocupa. E eu vou ser direto porque não sei ser de outro jeito.

Um estudo da Universidade de Stanford, publicado em agosto de 2025, analisou dados reais de folha de pagamento da ADP (o maior processador de folha de pagamento dos EUA) cobrindo milhões de trabalhadores. O resultado: o emprego de desenvolvedores de software entre 22 e 25 anos caiu quase 20% em relação ao pico do final de 2022⁹. Enquanto isso, o emprego de trabalhadores mais experientes nas mesmas funções se manteve estável ou cresceu.

Os pesquisadores identificaram que a IA é especialmente boa em substituir “conhecimento codificado”, ou seja, aquele conhecimento de livro-texto que vem da educação formal. Exatamente o que um junior dev tem. E é especialmente ruim em substituir conhecimento tácito, aquele que vem de anos lidando com problemas reais, clientes difíceis e sistemas que não se comportam como a documentação diz.

Eita, percebe o paradoxo? O caminho tradicional de formação de dev era: entra como junior, pega as tarefas mais simples, vai aprendendo com os seniors, e ao longo de anos acumula o conhecimento tácito que te torna um profissional experiente. Mas se a IA tá eliminando as tarefas simples (as mesmas que formavam os juniors), quem é que vai virar senior daqui a 5 anos?

Na aviação, esse problema já foi identificado. A Royal Aeronautical Society publicou um estudo alertando que a automação na cabine de pilotos está levando a uma degradação de habilidades básicas de pilotagem, e que muitos acidentes recentes simplesmente não teriam acontecido se os pilotos fossem capazes de habilidades básicas de voo manual¹⁰.

Faculdades, bootcamps e cursos de formação de devs precisam acordar pra essa realidade. Não dá mais pra formar gente que só sabe operar o autopilot. Precisa formar gente que entende o que acontece por baixo do capô, que sabe voar manual quando necessário, e que tem discernimento pra saber quando ligar e quando desligar a automação.

## Prepara o espírito: o que eu acho que vai acontecer

Olha, eu não tenho bola de cristal. Mas tenho mais de 20 anos de experiência no mercado de tech brasileiro e uma teimosia danada de olhar dados antes de opinar. Então vou te dizer o que eu vejo se desenhando.

**O dev que só “vibecoda” vai ser o piloto que só sabe apertar botão.** Funciona até o dia que não funciona. E quando não funcionar, vai ser um AF447 no seu sistema.

**As “horas de voo” vão se tornar mais importantes que o diploma.** Empresas vão começar a perguntar menos “o que você estudou?” e mais “o que você construiu? O que você operou? Que problemas reais você resolveu?”. O portfólio de projetos reais vai ser o log book do dev.

**O papel do senior vai mudar.** Menos “escrever código” e mais “garantir que o sistema voa seguro”. Review de código gerado por IA, decisões arquiteturais, mentoria de juniors que nunca tiveram que debugar um segfault na vida. O senior vira o comandante que não pilota o tempo todo, mas é responsável por tudo que acontece no voo.

**A formação precisa ser repensada do zero.** Não adianta enfiar IA nas universidades e achar que resolveu. Precisa ensinar os fundamentos primeiro, em voo manual, antes de ligar o autopilot. Precisa criar “horas de simulador” que sejam realmente desafiadoras, não exercícios triviais que a IA resolve em 3 segundos. O modelo de educação ainda é muito teórico e pouco prático.

## O voo continua. A questão é quem tá pilotando

Eu não sou contra IA em desenvolvimento de software. Seria burrice da minha parte. Autopilot tornou a aviação mais segura, mais eficiente e mais acessível. Ferramentas de IA estão fazendo o mesmo com software. Mas a aviação aprendeu, da pior forma possível (com vidas perdidas), que automação sem habilidade manual é uma bomba-relógio.

O voo AF447 não aconteceu porque a automação é ruim. Aconteceu porque, quando a automação falhou, os pilotos não tinham o repertório pra assumir. Não tinham as horas de voo manual. Não tinham o treino pra aquele cenário.

A pergunta que você deveria estar se fazendo não é “quanto de IA eu uso?”. É “quando foi a última vez que eu voei no manual?”.

Quando foi a última vez que você debugou um problema complexo sem pedir ajuda pra IA? Quando foi a última vez que você escreveu uma solução do zero, entendendo cada linha? Quando foi a última vez que você “pousou o avião” num incidente de produção confiando no seu conhecimento, e não num prompt?

Se você não lembra, prepara o espírito. Porque a próxima turbulência pode ser mais forte do que o autopilot aguenta.

Oxi oxi oxi… quem é que vai pousar esse avião?

---

*Esse foi um devaneio que nasceu de uma analogia que não sai da minha cabeça. Piloto e dev. Automação e habilidade. Simulador e mercado. Quanto mais eu fuço nos dados da aviação, mais eu vejo o futuro (e o presente) da engenharia de software ali, escrito em papel. A diferença é que a aviação paga suas lições com vidas. Em software, pagamos com sistemas frágeis, dívida técnica e profissionais que nunca aprenderam a voar de verdade. Prefiro aprender com quem já pagou o preço.  
  
Gostou desse? Assina aí meu povo que eu te mando mais no seu e-mail!*

---

**Fontes consultadas:**

¹ GitClear, “Comparing Developer AI Use Cohorts in 2026” (2026). Análise de 2.172 semanas de dados de desenvolvedores comparando uso de IA e código durável. https://www.gitclear.com/developer\_ai\_productivity\_analysis\_tools\_research\_2026

² Index.dev, “Top 100 Developer Productivity Statistics with AI Tools” (2025-2026). Compilação de estatísticas sobre adoção e impacto de ferramentas de IA. https://www.index.dev/blog/developer-productivity-statistics-with-ai-tools

³ Stack Overflow Developer Survey 2025. 49.000+ respostas de 177 países. 84% dos devs usam ou planejam usar ferramentas de IA. https://survey.stackoverflow.co/2025/

⁴ Bainbridge, L. (1983). “Ironies of Automation”. Automatica, 19(6), 775-779. https://www.sciencedirect.com/science/article/abs/pii/0005109883900468

⁵ Estudo sobre degradação cognitiva com automação em informação. Comparação de grupos manual vs. automação vs. alternado. 61% de degradação no grupo com automação. https://www.academia.edu/28945709/AN\_EVALUATION\_OF\_COGNITIVE\_SKILL\_DEGRADATION\_IN\_INFORMATION\_AUTOMATION

⁶ Pilot Pathfinder (2024). “Automation vs Manual Flying: Key Skill Gaps”. Baseado em múltiplos estudos sobre degradação de habilidades de pilotagem. https://blog.pilotpathfinder.com/automation-vs-manual-flying-key-skill-gaps/

⁷ METR (2025). “Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity”. RCT com 16 devs e 246 tarefas. https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/

⁸ ANAC (Agência Nacional de Aviação Civil). RBAC nº 61 - Licenças, habilitações e certificados para pilotos. Mínimo de 150 horas para licença de Piloto Comercial. Companhias aéreas brasileiras exigem entre 500 e 5.000 horas dependendo do mercado. https://www.gov.br/anac/pt-br/assuntos/regulados/profissionais-da-aviacao-civil/habilitacao/reducao-de-experiencia-para-obtencao-da-licenca-de-piloto-de-linha-aerea

⁹ Brynjolfsson, E., Chandara, A., & Chen, J. (2025). “Canaries in the Coal Mine? Six Facts about the Recent Decline in Entry-Level Employment”. Stanford Digital Economy Lab. https://digitaleconomy.stanford.edu/wp-content/uploads/2025/08/Canaries\_BrynjolfssonChandarChen.pdf

¹⁰ Royal Aeronautical Society Flying Operations Group. Estudo sobre degradação de habilidades de pilotagem com automação. Citado em Airline Ratings (2021). https://www.airlineratings.com/articles/cockpit-automation-leading-airline-industry-complacency

**Fontes complementares:**

- METR (2026). “We are Changing our Developer Productivity Experiment Design”. Atualização do estudo original com dados de 2026. https://metr.org/blog/2026-02-24-uplift-update/
- MIT Technology Review (2025). “AI coding is now everywhere. But not everyone is convinced.” https://www.technologyreview.com/2025/12/15/1128352/rise-of-ai-coding-developers-2026/
- Parasuraman, R., Sheridan, T., & Wickens, C. (2000). “A model of types and levels of human interaction with automation”. IEEE Trans. Syst., Man & Cybern.
- NASA/TM-2001-211413. “Examination of Automation-Induced Complacency and Individual Difference Variates”. https://ntrs.nasa.gov/api/citations/20020021642/downloads/20020021642.pdf
- Flight Safety Foundation (2021). “Lost Skills” - sobre degradação de habilidades de pilotagem com automação. https://flightsafety.org/asw-article/lost-skills/
- Collegiate Aviation Review International (2025). “Methods for Preventing the Degradation of Manual Flying Skills in an Automated Cockpit Environment”. https://ojs.library.okstate.edu/osu/index.php/CARI/article/view/10345
- ShiftMag (2026). “93% of Developers Use AI. Why Is Productivity Only 10%?” - dados de 4.2 milhões de devs. https://shiftmag.dev/this-cto-says-93-of-developers-use-ai-but-productivity-is-still-10-8013/
- Caso AF447: análise de fatores humanos e automação. https://humanfactors101.com/incidents/air-france-flight-447/