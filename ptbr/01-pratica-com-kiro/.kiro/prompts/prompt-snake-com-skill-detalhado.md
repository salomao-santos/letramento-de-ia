# Prompt: Snake Game COM Skill de Frontend Design (Versão Detalhada)

## Instrução para o Kiro (com a skill `frontend-design` ativada)

> **Nota:** Este prompt deve ser usado com a skill `frontend-design` habilitada no Kiro. A direção estética é altamente específica — fusão entre jogos retrô e tecnologia futurista/IA.

---

### Prompt:

Crie um jogo Snake completo, funcional e visualmente extraordinário em uma única página HTML (HTML + CSS + JS inline).

---

## Direção Estética e Conceito Visual

A identidade visual do jogo é inspirada nesta visão:

> *"Uma cobra gananciosa deslizando por um circuito impresso abstrato moderno, com código binário e componentes de computador ao fundo, representando a fusão entre jogos clássicos e tecnologia de IA de ponta. A cobra deve ser grande, imponente e vibrante, com uma aparência elegante e dinâmica. O fundo deve ter uma estética futurista e digital, com cores neon brilhantes e padrões de circuitos intrincados. O estilo geral deve ser uma mistura de elementos de jogos retrô e motivos contemporâneos de IA/tecnologia."*

### Estética: Retrofuturismo Digital / Circuito Neon

**Paleta de cores:**
- Fundo escuro profundo (preto azulado, #0a0e1a ou similar) simulando uma placa de circuito
- Neons vibrantes como destaques: verde elétrico (#00ff88), ciano (#00e5ff), magenta (#ff00c8), âmbar (#ffb700)
- A cobra deve ter um gradiente neon brilhante (verde → ciano) com efeito de glow/brilho
- A comida deve pulsar com brilho âmbar/dourado como um componente energizado
- Linhas de circuito sutis no fundo em tom baixo (#1a2040) que dão profundidade

**Tipografia:**
- Use fontes do Google Fonts que remetam a terminais e tecnologia, mas com personalidade — como `Orbitron` para títulos/pontuação e `JetBrains Mono` ou `Fira Code` para elementos secundários
- Números da pontuação devem ter efeito de glow neon
- Texto de game over com estética glitch ou digitalmente corrompida

**Fundo e atmosfera:**
- O tabuleiro do jogo deve parecer uma placa de circuito impresso abstrata
- Linhas finas formando trilhas de circuito no grid do jogo (sutis, em tom escuro)
- Partículas ou dígitos binários (0s e 1s) flutuando lentamente no fundo, semi-transparentes
- Efeito sutil de scanline ou CRT sobre toda a tela para reforçar o tom retro-tech
- Cantos do tabuleiro com "componentes" decorativos (pequenos quadrados/círculos simulando capacitores/chips)
- Efeito de vinheta escura nas bordas para foco central

**A cobra:**
- Cada segmento deve ser visualmente distinto (não apenas quadrados sólidos)
- Cabeça da cobra maior e mais detalhada que o corpo, com "olhos" brilhantes
- Corpo com gradiente que vai mudando de cor ao longo dos segmentos
- Efeito de rastro luminoso (trail/afterglow) ao se mover, como um circuito se iluminando
- Ao crescer, uma breve animação de "energia" percorre todo o corpo

**A comida:**
- Deve parecer um microchip ou componente eletrônico brilhante
- Pulsação contínua com glow (animação CSS)
- Ao ser coletada: explosão de partículas/fagulhas neon
- Pequeno efeito de "glitch" no score ao incrementar

**Animações e efeitos:**
- Entrada do jogo com revelação escalonada — linhas de circuito se "ligando" uma a uma
- Efeito de glitch/tremor na tela ao colidir (game over)
- Tela de game over com texto grande estilo "SYSTEM FAILURE" com animação glitch
- Transição suave ao reiniciar
- Hover nos botões com efeito de eletricidade/faísca
- Score com efeito de contagem rápida (counting up) ao pontuar

---

## Requisitos Funcionais

- A cobrinha se move continuamente na direção atual com velocidade que aumenta gradualmente
- Controle por setas do teclado (↑ ↓ ← →) e suporte a touch/swipe para mobile
- Comida aparece em posição aleatória (nunca sobre a cobra)
- Ao comer, a cobra cresce e a pontuação aumenta
- Game over ao colidir consigo mesma ou com as bordas
- Exibir pontuação atual e high score (persistido com localStorage)
- Botão estilizado para reiniciar após game over
- Responsivo — funciona em desktop e mobile
- Nível de dificuldade visual sutil (o fundo fica mais "energizado" conforme a pontuação sobe — mais partículas, brilho mais intenso)

---

## Requisitos Técnicos

- **Arquivo único:** HTML com CSS e JavaScript inline
- **Sem frameworks:** Vanilla HTML/CSS/JS
- **Dependências permitidas:** Apenas Google Fonts (Orbitron + JetBrains Mono ou similares)
- **Canvas API** para o jogo + **CSS** para UI/overlay/efeitos
- **Performance:** Animações suaves a 60fps, requestAnimationFrame para game loop

---

## Resumo da Visão

Este não é apenas um jogo Snake — é uma experiência visual que conta a história de uma cobra digital faminta devorando dados em uma placa-mãe futurista. Cada pixel deve respirar tecnologia. O jogador deve sentir que está dentro de um circuito vivo. O design deve ser tão marcante que alguém pausaria só para admirar a estética antes de jogar.

**Surpreenda. Impressione. Faça algo inesquecível.**
