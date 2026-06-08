---
title: "Code Review como Portão"
type: concept
tags: [code-review, qualidade, processo]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[wiki/sources/code-review-na-era-dos-agentes]]"]
---

# Code Review como Portão

## Papel na série

Terceiro pilar da camada 3, completando a tríade:
1. **Arquitetura** → por onde o agente pode ir
2. **Teste** → o que o agente deve produzir
3. **Code Review** → se pode passar (este conceito)

## Definição

O último portão humano antes de produção. Onde julgamento, intuição e conhecimento de negócio decidem se código gerado (por humano ou agente) pode se tornar permanente.

## O que SÓ o humano revisa

- Resolve o problema de negócio certo?
- Cabe na arquitetura combinada?
- O trade-off de design faz sentido?
- A abstração vai escalar?
- Tem alucinação de regra disfarçada de código bonito?

## O que a máquina já resolve

- Estilo e formatação
- Tipo errado
- Código duplicado
- Complexidade ciclomática
- Null check óbvio
- Padrão de segurança conhecido

## Fluxo ideal

```
CI (gates duros) → IA review (sensor) → Autor corrige → Humano revisa (juiz)
```

## Regras práticas

- PR de 200-400 linhas máximo
- Um propósito por PR
- IA é sensor, não juiz
- Se não consegue descrever como seria o erro, não está revisando

## Anti-padrões

- LGTM automático
- Bikeshedding (debater estilo, ignorar lógica)
- Scope insensitivity (mesmo esforço em 100 e 1000 linhas)
- Câmara de eco (mesmo modelo gera e revisa)

## Ver também

- [[wiki/concepts/tres-camadas-coding-ia]]
- [[wiki/concepts/automation-complacency]]
- [[wiki/concepts/sensores-computacionais]]
