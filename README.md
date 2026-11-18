# gha-cypress-run

![GitHub tag (latest by date)](https://img.shields.io/github/v/tag/Secuoyas-Experience/gha-cypress-run)

Esta acción ejecuta tests de Cypress con la caché que genera [Secuoyas-Experience/gha-cypress-cache](https://github.com/Secuoyas-Experience/gha-cypress-cache) y sube como artefacto (`cypress-<spec en base64>`, 2 días) las capturas, los vídeos y los resultados, que luego junta [Secuoyas-Experience/gha-cypress-report](https://github.com/Secuoyas-Experience/gha-cypress-report). El job falla si falla alguna spec; los artefactos se suben siempre.

## Requisitos

Desde la `v7` usa `actions/checkout@v7`, `actions/cache@v6` y `actions/upload-artifact@v7`, que se ejecutan con Node.js 24: el runner tiene que ser la versión 2.327.1 o posterior.

## Entradas

- **spec**: (obligatoria) spec o glob de specs de Cypress que se ejecutan.
- **cache-path**: (opcional) ruta de la caché de Cypress (por defecto `.cache/Cypress`).
- **browser**: (opcional) navegador (por defecto `chrome`; también vale `electron`).
- **tags**: (opcional) etiquetas de test separadas por comas, que se exportan como `CYPRESS_TEST_TAGS` (por defecto `regression`).

## Uso

En el siguiente ejemplo se usa `gha-cypress-run` después de `gha-cypress-cache`:

```yaml
name: cypress-run

on:
  workflow_dispatch:

jobs:
  cypress-cache:
    ...

  cypress-tests:
    runs-on: griddo-qa
    needs:
      - cypress-cache
    steps:
      - uses: Secuoyas-Experience/gha-cypress-run@v7
        with:
          spec: cypress/**/*.ts

  cypress-report:
    ...
```

También se pueden cambiar la ruta de la caché de Cypress, el navegador y las etiquetas:

```yaml
      - uses: Secuoyas-Experience/gha-cypress-run@v7
        with:
          cache-path: .cache/Cypress
          spec: cypress/**/*.ts
          browser: electron
          tags: regression,pages
```
