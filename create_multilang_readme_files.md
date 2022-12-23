## Как на GitHub вывести на главную страницу readme файл на другом языке:

- Создать readme файл на основном языке, например на русском `README.rst`
- Создать readme файл на другом языке, например на английском `README.en.rst`
- Создать директорию `.github` в корне репозитория
- Создать ссылку на `README.en.rst` в `.github`:
```
cd .github
ln -s /path/to/README.en.rst README.rst
```
- Если проект из репозитория загружается на PyPI, нужно скорректировать путь к readme файлу, который будет использовать PyPI, в `/setup.py` в переменной `long_description`
- Добавить в git `/.github/README.rst`
- Сделать commit и push

GitHub будет искать readme сначала в папке `/.github`, найдет и выведет `/.github/README.rst`. Он в свою очередь будет указывать на `README.en.rst`.

Если есть mirror репозитория (например на GitLab), то там на главной странице будет выводится readme файл на основном языке, т.е. `README.rst`.
