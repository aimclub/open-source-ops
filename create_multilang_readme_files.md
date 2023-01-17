## Как на GitHub вывести на главную страницу readme файл на другом языке:

- Создать readme файл на основном языке, например на русском `README.rst`
- Создать readme файл на другом языке, например на английском `README_en.rst`
- Создать директорию `.github` в корне репозитория
- Создать ссылку на `README_en.rst` в `.github`
  * На Linux:
  ```
  cd .github
  ln -s path/to/README_en.rst README.rst
  ```
  * На Windows:
    - открыть git консоль (например в IDE) и перейти в корень проекта 
    - выполнить команду:
    ```
    git config core.symlinks true
    ```
    - запустить `cmd.exe` от имени администратора и перейти в корень проекта 
    - выполнить команды:
    ```
    cd .github
    mklink README.rst path\to\README_en.rst
    ```

- Если проект из репозитория загружается на PyPI, нужно скорректировать путь к readme файлу, который будет использовать PyPI, в `setup.py` в переменной `long_description`
- Добавить в git `.github/README.rst`
- Сделать commit и push

GitHub будет искать readme сначала в папке `.github`, найдет и выведет `.github/README.rst`. Он в свою очередь будет указывать на `README_en.rst`.

Если есть mirror репозитория (например на GitLab), то там на главной странице будет выводиться readme файл на основном языке, т.е. `README.rst`.
