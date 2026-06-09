---
inclusion: manual
---

# Template: Transcrição de Vídeo YouTube

## Prompt genérico

Use este template como base para pedir transcrições de vídeos YouTube organizadas por minuto.

---

### Prompt

```
Passo 1 — Obtenha as informações do vídeo:
Use o MCP do YouTube (get_video_info) para buscar os metadados do vídeo:
[URL_DO_VIDEO]

Apresente para mim: título, canal/autor, descrição e idiomas de transcrição disponíveis.
Aguarde minha confirmação antes de prosseguir.

Passo 2 — Gere a transcrição:
Após confirmação, use get_timed_transcript para obter a transcrição com timestamps.

Crie um arquivo em raw/clippings/ com o seguinte formato:

1. Front-matter YAML com: title, author (canal/autor do vídeo), source (URL), type: transcript, date, language
2. Título H1 com nome da palestra/vídeo e autor
3. Conteúdo dividido por minuto (## Minuto 0, ## Minuto 1, etc.)
4. Cada segmento com timestamps simplificados [MM:SS]
5. Se o vídeo for longo (>20min), use sub-agentes para paralelizar a criação

Se o idioma disponível for diferente do esperado, use o que estiver disponível e indique no front-matter.
```

---

### Variações úteis

**Com resumo por seção:**
```
Além da transcrição por minuto, adicione um resumo de 1-2 frases no início de cada segmento de minuto descrevendo o tema abordado.
```

**Com extração de conceitos:**
```
Após a transcrição, adicione uma seção "## Conceitos-chave" listando os principais termos e ideias mencionados, com o timestamp de onde aparecem.
```

**Com tradução:**
```
A transcrição está em [IDIOMA_ORIGINAL]. Crie duas versões:
1. Transcrição original por minuto
2. Tradução para português por minuto
```

---

### Parâmetros

| Parâmetro | Descrição | Exemplo |
|-----------|-----------|---------|
| URL_DO_VIDEO | Link do YouTube | https://www.youtube.com/watch?v=XXXXX |
| IDIOMA | Código do idioma preferido | pt, en, es |
| PASTA_DESTINO | Onde salvar o arquivo | raw/clippings/ |
| COM_RESUMO | Incluir resumo por minuto | sim/não |
| COM_CONCEITOS | Extrair conceitos-chave | sim/não |
