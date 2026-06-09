---
title: "ArchUnit"
type: entity
tags: [ferramenta, java, arquitetura, sensor-computacional]
created: 2026-06-08
updated: 2026-06-08
sources: ["[[wiki/sources/arquitetura-na-era-dos-agentes]]"]
---

# ArchUnit

## O que é

Biblioteca para Java que permite escrever testes de arquitetura que rodam como JUnit. Valida direção de dependência entre camadas.

## Exemplo

```java
layeredArchitecture()
    .consideringAllDependencies()
    .layer("Controllers").definedBy("..controller..")
    .layer("Services").definedBy("..service..")
    .layer("Repositories").definedBy("..repository..")
    .whereLayer("Controllers").mayNotBeAccessedByAnyLayer()
    .whereLayer("Services").mayOnlyBeAccessedByLayers("Controllers")
    .whereLayer("Repositories").mayOnlyBeAccessedByLayers("Services")
    .check(classes);
```

## Papel na era dos agentes

Sensor computacional determinístico. Se o agente (ou humano) tentar criar dependência proibida, o build quebra. Sem discussão, sem exceção.

## Recomendação

Rodar como **teste** (quebra build), não como lint (só avisa).

## Ver também

- [[wiki/entities/dependency-cruiser]] — equivalente para JavaScript/TypeScript
- [[wiki/concepts/sensores-computacionais]]

## Links

- Site: https://www.archunit.org/
