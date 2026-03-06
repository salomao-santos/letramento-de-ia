# Linha do tempo: evolução do desenvolvimento de software

Esta seção mapeia a evolução completa: desde código sem IDE, passando pela era das IDEs, até a IA generativa adaptativa.

## Linha do tempo visual

```mermaid
%%{init: {"themeVariables": {"fontSize": "18px"}, "flowchart": {"nodeSpacing": 50, "rankSpacing": 50}}}%%
flowchart LR
	A["📝 Antes de 2000<br/>Código sem IDE<br/>Editor de texto + Compilador"] --> B["💻 2000-2020<br/>Com IDE<br/>Autocompletar, debug visual"] --> C["🤖 2023<br/>LLM Assistants<br/>Auto-complete IA"] --> D["🔧 2024<br/>MCP + Tools<br/>Protocolo padrão"] --> E["⚡ 2025<br/>Progressive Disclosure<br/>Contexto dinâmico"] --> F["🎯 2026+<br/>Adaptive Context<br/>Auto-otimizável"]
```

## Antes de 2000: código sem IDE

Desenvolvimento puro em editor de texto (Vim, Emacs) com compilador manual. Sem autocompletar, sem debug visual, sem contexto automático.

**Características:**
- Editor de texto simples
- Compilação manual via terminal
- Documentação em papel ou HTML
- Todo o contexto na cabeça do desenvolvedor
- Sem controle visual de erros

```mermaid
%%{init: {"themeVariables": {"fontSize": "20px"}, "flowchart": {"nodeSpacing": 60, "rankSpacing": 60}}}%%
flowchart LR
	A[Texto puro] --> B[Compilador manual]
	B --> C[Sem feedback visual]
	C --> D[Contexto memorizado]
```

## 2000-2020: era da IDE (Integrated Development Environment)

Surgem as IDEs modernas (Visual Studio, Eclipse, IntelliJ). Autocompletar baseado em sintaxe, debug visual, gestão de projetos integrada.

**Características:**
- Autocompletar baseado em árvore sintática
- Debug visual com breakpoints
- Gerenciador de projetos integrado
- Contexto organizado em abas e painéis
- Erro em tempo real (warnings/erros)

```mermaid
%%{init: {"themeVariables": {"fontSize": "20px"}, "flowchart": {"nodeSpacing": 60, "rankSpacing": 60}}}%%
flowchart LR
	A[IDE] --> B[Auto-complete sintático]
	A --> C[Debug visual]
	A --> D[Gerenciador de arquivos]
	B --> E[Contexto visual do projeto]
	C --> E
	D --> E
```

## 2023: LLM Assistants (auto-complete com IA)

Surgem GitHub Copilot, ChatGPT, Claude. Auto-complete agora usa redes neurais treinadas em bilhões de linhas de código. Contexto passa a ser entendido semanticamente.

**Características:**
- Auto-complete com IA (padrões aprendidos)
- Chat com o código
- Entendimento semântico, não só sintático
- Geração de funções/classes inteiras
- Contexto da sessão atual (histórico)

```mermaid
%%{init: {"themeVariables": {"fontSize": "20px"}, "flowchart": {"nodeSpacing": 60, "rankSpacing": 60}}}%%
flowchart LR
	A[IDE + LLM] --> B[Auto-complete semântico]
	A --> C[Chat com código]
	A --> D[Geração inteligente]
	B --> E[Contexto semântico]
	C --> E
	D --> E
```

**Exemplo: GitHub Copilot em 2023**
- Contexto: arquivo aberto + histórico de escrita
- Saída: linha/função sugerida
- Limite: tudo precisa ser carregado/revisado

## 2024: Tool Use + MCP (ferramentas estáticas com protocolo padrão)

Em 2024, surgem os primeiros padrões de conexão entre agentes e ferramentas. O MCP (Model Context Protocol) estabelece um padrão para que LLMs acessem ferramentas de forma consistente. O contexto ainda é basicamente estático, mas agora pode ser compartilhado estruturadamente.

**Características:**
- Ferramentas com descritores completos
- Protocolo padrão (MCP)
- Contexto ainda manualmente carregado
- Agentes com ferramentas fixas

```mermaid
%%{init: {"themeVariables": {"fontSize": "20px"}, "flowchart": {"nodeSpacing": 60, "rankSpacing": 60}}}%%
flowchart TB
	A[Agente LLM] --> B[MCP: Protocolo padrão]
	B --> C1[Ferramenta 1]
	B --> C2[Ferramenta 2]
	B --> C3[Ferramenta 3]
	C1 --> D[Contexto estático carregado manualmente]
	C2 --> D
	C3 --> D
```

**Vantagens:**
- Padronização entre ferramentas
- Melhor integração com LLMs
- Contexto estruturado

**Limitações:**
- Contexto ainda manual
- Sem adaptação automática
- Sem memória hierárquica

## 2025: Progressive Disclosure (contexto dinâmico carregado sob demanda)

Em 2025, o contexto se torna dinâmico. Em vez de carregar tudo de uma vez, o sistema carrega contexto sob demanda. Ferramentas como "lazy loading" de agentes e histórico consultável transformam como usamos contexto.

**Características:**
- Carregamento sob demanda (lazy loading)
- Subagentes com contexto isolado
- Histórico consultável como arquivo
- Contexto progressivo (começa mínimo, expande conforme necessário)

```mermaid
%%{init: {"themeVariables": {"fontSize": "20px"}, "flowchart": {"nodeSpacing": 60, "rankSpacing": 60}}}%%
flowchart TB
	A[Agente principal] --> B{Necessita contexto?}
	B -->|Sim| C[Carrega sob demanda]
	B -->|Não| D[Segue sem carregar]
	C --> E[Histórico consultável]
	E --> F[Contexto isolado por subagente]
	D --> G[Executa com contexto mínimo]
```

**Vantagens:**
- Menos desperdício de tokens
- Contexto mais relevante
- Melhor escalabilidade

## 2026+: Adaptive Context (contexto auto-otimizável)

A partir de 2026, o contexto se torna verdadeiramente adaptativo. O sistema otimiza automaticamente o que precisa de contexto, cria memória hierárquica e aprende com o uso.

**Características:**
- Orquestração multi-agente inteligente
- Contexto auto-otimizável
- Memória hierárquica (curta/longa prazo)
- Contexto aprende com uso

```mermaid
%%{init: {"themeVariables": {"fontSize": "20px"}, "flowchart": {"nodeSpacing": 60, "rankSpacing": 60}}}%%
flowchart TB
	A[Sistema adaptativo] --> B[Memória de curto prazo]
	A --> C[Memória de longo prazo]
	B --> D[Contexto auto-otimizável]
	C --> D
	D --> E[Aprende com feedback]
	E --> F[Melhora automática]
	F --> A
```

**Vantagens:**
- Menos intervenção manual
- Contexto sempre relevante
- Melhoria contínua

## Resumo: Evolução do contexto

| Período | Nome | Contexto | Adaptação | Escalabilidade |
|---------|------|----------|-----------|---|
| Antes de 2023 | Manual | Estático/Manual | Nenhuma | Baixa |
| 2024 | Tool Use + MCP | Estático/Padrão | Manual | Média |
| 2025 | Progressive Disclosure | Dinâmico/Sob demanda | Parcial | Alta |
| 2026+ | Adaptive Context | Adaptativo/Auto-otimizável | Automática | Muito alta |

