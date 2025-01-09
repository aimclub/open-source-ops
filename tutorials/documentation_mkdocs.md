# Руководство по документированию проекта - MkDocs Material

## Введение
MkDocs - это статический генератор сайтов, предназначенный для создания документации. MkDocs Material - это тема для MkDocs, которая предоставляет множество возможностей для создания красивой и функциональной документации.
При создании документации документации mkdocs, документация хостится на GitHub Pages. Это позволяет не создавать дополнительных аккаунтов, быстрее и удобнее вносить изменения в документацию.

## Установка и настройка
Для установки MkDocs Material необходимо выполнить следующцю команду:

```bash
pip install mkdocs-material 'mkdocstrings[python]'
```

Для дальнейшей настройки необходимо создать файл конфигурации `mkdocs.yml` в корневой директории проекта. Пример файла конфигурации:

```yaml
site_name: myproject
repo_name: myusername/myproject
repo_url: https://github.com/myusername/myproject
theme:
  name: material
  locale: en
  features:
    - announce.dismiss
    - content.action.edit
    - content.action.view
    - content.code.annotate
    - content.code.copy
    - content.code.select
    - content.footnote.tooltips
    - content.tabs.link
    - content.tooltips
    - header.autohide
    - navigation.expand
    - navigation.footer
    - navigation.indexes
    - navigation.instant
    - navigation.instant.prefetch
    - navigation.instant.progress
    - navigation.prune
    - navigation.sections
    - navigation.tabs
    - navigation.tabs.sticky
    - navigation.top
    - navigation.tracking
    - search.highlight
    - search.share
    - search.suggest
    - toc.follow
    - toc.integrate
  palette:
    - media: "(prefers-color-scheme)"
      toggle:
        icon: material/link
        name: Switch to light mode
    - media: "(prefers-color-scheme: light)"
      scheme: default
      primary: indigo
      accent: indigo
      toggle:
        icon: material/toggle-switch
        name: Switch to dark mode
    - media: "(prefers-color-scheme: dark)"
      scheme: slate
      primary: black
      accent: indigo
      toggle:
        icon: material/toggle-switch-off
        name: Switch to system preference
  font:
    text: Roboto
    code: Roboto Mono

nav:
  - Home: index.md
  - Getting Started: user-guide/getting-started.md
  - Installation: user-guide/installation.md
  - API Reference:
      - api-reference.md
      - mymodule: mymodule.md
      - mypackage: mypackage.md
extra:
  social:
    - icon: fontawesome/brands/github
      link: https://github.com/myusername/myproject
plugins:
  - search
  - mkdocstrings
markdown_extensions:
  - admonition
  - codehilite
  - footnotes
  - meta
  - toc:
      permalink: True
```

Чтобы документация автоматически обновлялась на GitHub Pages, необходимо добавить в файл `.github/workflows/mkdocs.yml` следующий код:

```yaml
name: mkdocs
on:
  push:
    branches:
      - master
      - main
permissions:
  contents: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Configure Git Credentials
        run: |
          git config user.name github-actions[bot]
          git config user.email 41898282+github-actions[bot]@users.noreply.github.com
      - uses: actions/setup-python@v5
        with:
          python-version: 3.x
      - run: echo "cache_id=$(date --utc '+%V')" >> $GITHUB_ENV
      - uses: actions/cache@v4
        with:
          key: mkdocs-material-${{ env.cache_id }}
          path: .cache
          restore-keys: |
            mkdocs-material-
      - run: pip install mkdocs-material 'mkdocstrings[python]'
      - run: mkdocs gh-deploy --force
```

## Использование

### Добавление страниц
В корне папки `docs` создайте файл `index.md`. Это будет главная страница документации. Для добавления новой страницы создайте новый файл с расширением `.md` в папке `docs`.

Таким образом, структура проекта документации может выглядеть следующим образом:

```
    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        user-guide/
            getting-started.md
            installation.md
        api-reference.md
        mymodule.md
        mypackage.md
        ...       # Other markdown pages, images and other files.
```

### Добавление изображений
Для добавления изображений, их можно поместить в папку `docs` или в папку `docs/images`. Для добавления изображения на страницу документации, используйте следующий синтаксис:

```markdown
![Alt text](path/to/image.png)
```

### Остальное
Так как MkDocs полностью поддерживает markdown, вы можете использовать все возможности markdown для форматирования текста, добавления ссылок, списков, таблиц и т.д.
Однако, для использования некоторых возможностей, может понадобится установка расширений через поле `markdown_extensions` в `mkdocs.yml`.

## Тестирование и развертывание

### Тестирование
Для тестирования документации локально, выполните следующую команду:

```bash
mkdocs serve
```

После выполнения команды, документация будет доступна по адресу, указанному в терминале. 

### Развертывание

Для развертывания на GitHub Pages, достаточно просто запушить изменения в репозиторий. Документация будет доступна по адресу `https://myusername.github.io/myproject/`.

## Заключение

Для более подробных инструкций можно использовать:

- [MkDocs](https://www.mkdocs.org/)
- [MkDocs Material](https://squidfunk.github.io/mkdocs-material/)

## Примеры

Такая документация уже используется на одном из проектов лаборатории. Однако работа над проектом еще ведется, поэтому документация пока в начальном виде. Но уже можно посмотреть на интерфейс и некоторые страницы документации.

- [applyBN (WIP)](https://anaxagor.github.io/applyBN/)
