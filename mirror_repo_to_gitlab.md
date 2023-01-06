# Настройка зеркала репозитория с GitHub на GitLab

В этом репозитории хранится Github Actions [workflow](/.github/workflows/mirror-repo.yml), 
который поддерживает зеркало GitHub репозитория на GitLab.

Как использовать [workflow](/.github/workflows/mirror-repo.yml), чтобы настроить зеркало для вашего репозитория:

- Убедитесь, что у вашего пользователя статус `Maintainer` или `Owner` на уровне группы. 
  Если нет, попросите администратора изменить статус.

- Импортируйте проект на GitLab:
  - Перейдите на https://gitlab.actcognitive.org/
  - В правом верхнем углу нажмите на `New project`
  - Выберите `Import project`
  - Выберите `GitHub`
  - Введите ваш `access token` (его можно сгенерировать по [инструкции](https://docs.github.com/en/enterprise-server@3.4/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token), название может быть любым, срок действия обычно выставляют до одного года, среди `scopes` обязательно надо выбрать `repo`)
  - Найдите в списке ваш проект
  - Задайте рядом с ним вашу группу на GitLab (для проектов NSS Lab используйте [ITMO-NSS-team](https://gitlab.actcognitive.org/itmo-nss-team))
    ![alt text](/images/gitlab_group.jpg)
  - Нажмите `Import`

- Уберите ветку main из списка защищённых:
  - На GitLab откройте ваш проект
  - Откройте `Settings` => `Repository`
  - В разделе `Protected branches` найдите в списке ветку `main` и нажмите `Unprotect`

- Задайте секреты `GITLAB_USER` и `GITLAB_PASSWORD` в вашем репозитории на GitHub.
  Если у вас несколько открытых репозиториев внутри одной организации, можно задать секреты на уровне организации,
  тогда все открытые репозитории их унаследуют. Для приватных всегда секреты надо задавать на уровне репозитория.
  - Откройте ваш репозиторий/организацию
  - Откройте раздел `Settings`
  - Слева выберите `Security` => `Secrets` => `Actions`
  - Создайте секреты 

- В репо на GitHub создайте файл `/.github/workflows/mirror_repo_to_gitlab.yml` с таким содержанием:
```
name: Mirror repo to GitLab

on: [push, pull_request, delete]

jobs:
  call-nss-ops-mirror-workflow:
    uses: ITMO-NSS-team/NSS-Ops/.github/workflows/mirror-repo.yml@master
    with:
      GITLAB_URL: '<gitlab_repo_web_URL>'
    secrets:
      GITLAB_USER: ${{ secrets.GITLAB_USER }}
      GITLAB_PASSWORD: ${{ secrets.GITLAB_PASSWORD }}
```

- Не забудьте подставить нужное значение в `GITLAB_URL`.

- Параметр `uses: ITMO-NSS-team/NSS-Ops/.github/workflows/mirror-repo.yml@master` менять НЕ надо.

Каждый push в репозиторий будет автоматически запускать этот action. Все commit-ы и ветки будут синхронизованы автоматически.
PR-ы, issue и wiki НЕ будут синхронизированы.

При импорте репозитория на GitLab через UI, issue и PR-ы также будут скопированы, 
но все дальнейшие их изменения НЕ будут синхронизироваться.



