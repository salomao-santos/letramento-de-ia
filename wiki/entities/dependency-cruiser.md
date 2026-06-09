---
title: "dependency-cruiser"
type: entity
tags: [ferramenta, javascript, typescript, arquitetura, sensor-computacional]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[wiki/sources/arquitetura-na-era-dos-agentes]]"]
---

# dependency-cruiser

## O que é

Ferramenta para JavaScript/TypeScript que valida e visualiza dependências entre módulos. Equivalente ao [[wiki/entities/archunit]] para o ecossistema JS/TS.

## Exemplo de configuração

```json
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

## Papel na era dos agentes

Barra dependências proibidas no CI. Se o agente tentar puxar cliente HTTP para dentro do use case, o CI trava.

## Ver também

- [[wiki/entities/archunit]] — equivalente para Java
- [[wiki/concepts/sensores-computacionais]]

## Links

- GitHub: https://github.com/sverweij/dependency-cruiser
