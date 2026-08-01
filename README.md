name: Gerar animação da snake

on:
  schedule:
    - cron: "0 */12 * * *"   # a cada 12 horas
  workflow_dispatch:          # botão manual
  push:
    branches:
      - main

jobs:
  generate:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Gerar SVGs da snake
        uses: Platane/snk@v3
        id: snake-gif
        with:
          github_user_name: ismaellnog
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark

      - name: Publicar na branch output
        uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
