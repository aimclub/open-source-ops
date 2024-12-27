# Автоформатирование кода в репозитории с помощью Black

> [!TIP]
> Black — это инструмент для автоматического форматирования кода на Python. Он позволяет сделать код более читаемым и улучшить его структуру.

Автоформатирование кода избавляет от рутинного процесса ручного выравнивания кода и позволяет сосредоточиться на более важных задачах. Black — один из самых популярных инструментов для автоформатирования кода на Python.

Для локального использования Black необходимо установить его с помощью менеджера пакетов pip:

```bash
pip install black
```

Или для поддержки форматирования Jupyter-ноутбуков:

```bash
pip install "black[jupyter]"
```

После установки Black можно использовать его для форматирования кода в файлах и директориях. Например, чтобы отформатировать файл `example.py`, необходимо выполнить команду:

```bash
black example.py
black my_project/
```

Для репозиториев на GitHub можно использовать GitHub Actions для автоматического форматирования кода при создании Pull Request. Для этого необходимо добавить следующий workflow в файл `.github/workflows/black.yml`:

```yaml
name: black-action
on: [push, pull_request]
jobs:
  linter_name:
    name: Run black formatter
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: rickstaa/action-black@v1.3.3
        with:
          black_args: "."
```
