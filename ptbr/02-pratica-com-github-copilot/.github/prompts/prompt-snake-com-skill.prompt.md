# Prompt: Snake Game COM Skill de Frontend Design

## Instrução para o GitHub Copilot (com a skill `frontend-design` e a instruction `html-css-style-color-guide` ativadas)

> **Nota:** Este prompt deve ser usado com a skill `frontend-design` e a instruction `html-css-style-color-guide` habilitadas no GitHub Copilot, garantindo que o design visual siga as diretrizes estéticas avançadas da skill e as regras de cores da instruction.

> **Como usar:** No VS Code, abra o Copilot Chat (Agent mode), clique no ícone de "prompt" (📎) e selecione este prompt. As referências à skill e à instruction abaixo serão automaticamente incluídas no contexto.

---

### Referências de contexto

- [skill-ptbr.md](../skills/frontend-design/skill-ptbr.md)
- [html-css-style-color-guide.instructions.md](../instructions/html-css-style-color-guide.instructions.md)

---

### Prompt:

Crie um jogo Snake completo e funcional em uma única página HTML (HTML + CSS + JS inline).

**Requisitos funcionais:**
- A cobrinha se move continuamente na direção atual
- O jogador controla a direção com as setas do teclado (↑ ↓ ← →)
- Uma "comida" aparece em posição aleatória no tabuleiro
- Ao comer a comida, a cobrinha cresce e a pontuação aumenta
- O jogo termina se a cobrinha colidir consigo mesma ou com as bordas
- Exibir pontuação atual e recorde (high score) usando localStorage
- Botão para reiniciar o jogo após game over
- O jogo deve ser responsivo e funcionar bem em desktop e mobile (suporte a touch/swipe)

**Requisitos de design (a skill frontend-design vai guiar isso):**
- Aplique uma direção estética OUSADA e memorável — NÃO use design genérico
- Tipografia distintiva (fontes do Google Fonts que sejam únicas e interessantes)
- Paleta de cores coesa com acentos dramáticos
- Animações e micro-interações (efeitos ao comer comida, transição de game over, entrada escalonada)
- Fundo com atmosfera e profundidade (gradientes, texturas, grão)
- Layout com composição espacial interessante (não apenas um canvas centralizado sem contexto)
- Tela de game over estilizada com animação

**Stack:** HTML único com CSS e JavaScript inline. Sem dependências externas além de Google Fonts.

**Pasta de destino:** Salve o arquivo gerado na pasta `snake-com-skill/` na raiz do projeto (caminho: `snake-com-skill/index.html`).

Surpreenda-me com o design. Quero algo que pareça ter sido feito por um designer criativo, não por uma IA genérica.
