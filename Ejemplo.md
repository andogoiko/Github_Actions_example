name: push en rama

on:
  push:
    branches:
      - rama # cada vez que se haga push a la rama se ejecutará
  workflow_dispatch:

env:
  ejecuta: true

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      # buildea la aplicación aquí

      - name: Set outputs
        id: set_outputs
        run: |
          echo "::set-output name=commit_exists::${COMMIT_EXISTS}"

  ensure:
    needs: build
    runs-on: ubuntu-latest
    if: needs.build.outputs.commit_exists != 'true'

    steps:
      # ejecuta las acciones necesarias