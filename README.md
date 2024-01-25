# gha-cypress-run

![GitHub tag (latest by date)](https://img.shields.io/github/v/tag/Secuoyas-Experience/gha-cypress-run)

Esta accion permite ejecutar tests de Cypress utilizando la cache proporcionada por [Secuoyas-Experience/gha-cypress-cache](https://github.com/Secuoyas-Experience/gha-cypress-cache) y crea artefactos con los informes que se pueden mergear con [Secuoyas-Experience/gha-cypress-report](https://github.com/Secuoyas-Experience/gha-cypress-run).

## Documentacion

## Inputs

- **cache-path**: (optional) where is located Cypress cache (default is .cache/Cypress)
- **browser**: (optional) type of browser to use (only chrome is available at the moment)
- **spec**: Cypress spec to execute

## Usage

En el siguiente ejemplo se muestra como utilizar el action `gha-cypress-run`:

```yaml
name: cypress-run

on:
  workflow_dispatch:

jobs:
  cypress-cache:
    ...

  cypress-tests:
    steps:
      - uses: Secuoyas-Experience/gha-cypress-run@v3
        with:
          spec: cypress/**/*.ts

  cypress-report:
    ...
```

Tambien se puede cambiar los parametros de cache de Cypress y de retencion de los informes

```yaml
name: cypress-run

on:
  workflow_dispatch:

jobs:
  cypress-cache:
    ...

  cypress-tests:
    steps:
      - uses: Secuoyas-Experience/gha-cypress-run@v3
        with:
          cache-path: .cache/Cypress
          spec: cypress/**/*.ts
          browser: chrome

  cypress-report:
    ...
```