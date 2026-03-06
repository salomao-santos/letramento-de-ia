# Introdução

Esta introdução abre a apresentação sobre Letramento de IA.

Antes de entrar em IA generativa, é útil lembrar que toda linguagem (natural ou de programação) tem estrutura. Todo idioma costuma seguir a estrutura de artigo, sujeito, verbo e objetos, e chamamos isso de sintaxe. Isso não é só forma: é a base para o significado. Em computação, a ideia é parecida: toda linguagem tem sintaxe (as regras de escrita) e semântica (o que aquilo significa).

## Idioma (exemplo)

#### Language (English): "The student studied the content with attention."

```mermaid
%%{init: {"themeVariables": {"fontSize": "20px"}, "flowchart": {"nodeSpacing": 50, "rankSpacing": 50}}}%%
flowchart TB
	A[Language] --> B[Syntax: form]
	A --> C[Semantics: meaning]

	B --> BE[English]
	BE --> E1[Article]
	E1 --> E1a[The]
	BE --> E2[Subject]
	E2 --> E2a[student]
	BE --> E3[Verb]
	E3 --> E3a[studied]
	BE --> E4[Direct object]
	E4 --> E4a[content]
	BE --> E5[Indirect object]
	E5 --> E5a[with attention]

	C --> C1[Who?]
	C1 --> C1a[the student]
	C --> C2[What did?]
	C2 --> C2a[studied]
	C --> C3[What?]
	C3 --> C3a[the content]
	C --> C4[How?]
	C4 --> C4a[with attention]
```

#### Idioma (PT-BR): "O aluno estudou o conteúdo com atenção."

```mermaid
%%{init: {"themeVariables": {"fontSize": "20px"}, "flowchart": {"nodeSpacing": 50, "rankSpacing": 50}}}%%
flowchart TB
	A[Idioma] --> B[Sintaxe: forma]
	A --> C[Semântica: significado]

	B --> BP[Português]
	BP --> B1[Artigo]
	B1 --> B1a[O]
	BP --> B2[Sujeito]
	B2 --> B2a[aluno]
	BP --> B3[Verbo]
	B3 --> B3a[estudou]
	BP --> B4[Objeto direto]
	B4 --> B4a[conteúdo]
	BP --> B5[Objeto indireto]
	B5 --> B5a[com atenção]

	C --> C1[Quem?]
	C1 --> C1a[o aluno]
	C --> C2[O que fez?]
	C2 --> C2a[estudou]
	C --> C3[O que?]
	C3 --> C3a[o conteúdo]
	C --> C4[Como?]
	C4 --> C4a[com atenção]
```



## Linguagem de programação (visão geral)

Assim como no idioma, linguagens de programação têm partes fixas e regras claras. Em geral, toda linguagem possui declaração de variáveis, funções ou métodos, e segue um ou mais paradigmas. Além disso, pode ser classificada por tipos, grau de abstração e geração.

```mermaid
%%{init: {"themeVariables": {"fontSize": "28px"}, "flowchart": {"nodeSpacing": 80, "rankSpacing": 80}}}%%
flowchart TB
	L[Linguagem de Programação]

	L --> P[Paradigma]
	P --> PI[Imperativo]
	PI --> PI1[Procedural]
	PI --> PI2[Estrutura de blocos]
	PI --> PI3[Orientação a objetos]
	PI --> PI4[Computação distribuída]
	P --> PD[Declarativo]
	PD --> PD1[Funcional]
	PD --> PD2[Programação lógica]

	L --> T[Estrutura de Tipos]
	T --> T1[Fracamente tipada]
	T --> T2[Fortemente tipada]
	T --> T3[Dinamicamente tipada]
	T --> T4[Estaticamente tipada]

	L --> A[Grau de Abstração]
	A --> A1[Baixo nível]
	A --> A2[Médio nível]
	A --> A3[Alto nível]
```

Com essa base, fica mais fácil entender IA generativa como uma tecnologia que aprende a produzir linguagem (texto, código, imagens e áudio) seguindo regras, contexto e significado.

## Fluxo tradicional de desenvolvimento (antes da IA)

Antes da IA generativa, o caminho mais comum para transformar uma ideia em software era mais linear e manual: entender o problema, detalhar requisitos, desenhar a solução, escrever o código e testar. Esse fluxo reforça a importância da clareza de objetivos e da comunicação entre pessoas, pois o computador executa exatamente o que foi especificado.

```mermaid
%%{init: {"themeVariables": {"fontSize": "20px"}, "flowchart": {"nodeSpacing": 60, "rankSpacing": 70}}}%%
flowchart LR
	subgraph Humano[Parte humana]
		direction LR
		A[Ideia] --> B[Problema]
		B --> C[Requisitos]
		C --> D[Design/Arquitetura da solução]
		D --> E[Algoritmo]
		E --> F[Desenvolvimento com uso da IDE]
		F --> G[Código-fonte]
	end

	subgraph Maquina[Parte da máquina]
		direction LR
		H[Compilador/Interpretador] --> I[Programa]
		I --> J[Execução pela máquina]
	end

	G --> H
```

## Por que o algoritmo é tão importante

O algoritmo é o passo a passo que transforma uma intenção em uma sequência executável. Ele organiza o raciocínio, reduz ambiguidades e permite que a mesma tarefa seja repetida com consistência. Em outras palavras, sem algoritmo não existe software confiável: existe só uma ideia vaga que a máquina não consegue executar.

```mermaid
%%{init: {"themeVariables": {"fontSize": "20px"}, "flowchart": {"nodeSpacing": 60, "rankSpacing": 60}}}%%
flowchart TD
	A[Objetivo: escovar os dentes] --> B{Tem fio dental?}
	B -->|Sim| C[Passar o fio dental]
	B -->|Não| D[Seguir sem fio dental]
	C --> E[Pegar a escova]
	D --> E
	E --> F[Colocar creme dental]
	F --> G[Abrir a torneira]
	G --> H[Escovar os dentes]
	H --> I[Lavar a escova]
	I --> J[Fechar a torneira]
	J --> K[Fim]
```
