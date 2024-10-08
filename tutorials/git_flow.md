# Основные use-cases git

Git - это распределенная система управления версиями, разработанная Линусом Торвальдсом. Эта технология позволяет разработчикам сохранять все версии своего проекта и легко возвращаться к предыдущим состояниям. Особенно важным аспектом Git является возможность создания веток, что значительно облегчает совместную работу над проектами. Аналогами Git являются такие системы управления версиями, как Subversion, Perforce, Bazaar, которые также предоставляют средства для контроля за изменениями в проектах. Однако Git выделяется своей популярностью и масштабностью, широко используется в разнообразных областях разработки, и для работы с ним существует множество платформ, включая GitHub, GitLab, Bitbucket. Git позволяет разработчикам с легкостью сотрудничать, а также применяется не только для кода, но и для работы с различными типами файлов.

Ниже располагаются основные концепции и компоненты Git, которые необходимо понимать:
- Репозиторий (Repository) - это хранилище всех файлов, истории изменений и метаданных проекта. Он содержит все коммиты, ветки, теги и конфигурационные файлы. Репозиторий может быть локальным или удаленным;
- Коммит (Commit) - сохраненное состояние проекта в определенный момент времени. Коммит содержит информацию о внесенных изменениях, авторе, дате и сообщении коммита. Коммиты являются основными строительными блоками в истории проекта и образуют дерево коммитов. В качестве общепринятого стиля коммитов можно использовать [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/);
- Ветка (Branch) - это легковесная подвижная ссылка на коммит. Ветки позволяют разработчикам работать над разными фичами или исправлениями ошибок параллельно, не затрагивая основную линию разработки. Каждая ветка имеет свою собственную историю коммитов;
- Ветвление (Branching) - это создание новой ветки на основе существующей. Это позволяет разработчикам работать над различными фичами или задачами независимо друг от друга. Каждая ветка имеет свою собственную историю коммитов и изменения в одной ветке не влияют на другие ветки.
- Слияние (Merge) позволяет объединить изменения из одной ветки с другой. При слиянии Git автоматически интегрирует изменения из двух разных веток, результирующий коммит объединяет изменения обеих веток;
- Удаленный репозиторий (Remote Repository) - это репозиторий, расположенный на удаленном сервере или в облачном хранилище. Он предоставляет доступ к репозиторию другим разработчикам для совместной работы над проектом. Удаленный репозиторий позволяет разработчикам обмениваться коммитами и синхронизировать изменения;
- Клонирование (Clone) - создание локальной копии удаленного репозитория. Клонирование позволяет разработчику получить полную копию истории, файлов и веток проекта, которую можно изменять и коммитить локально;
- Форк (Fork) - это копия удаленного репозитория, созданная разработчиком с целью внести собственные изменения в проект. Форк позволяет работать над проектом независимо от исходного репозитория;
- Запрос на слияние (Pull Request) - это концепция, специфичная для систем управления версиями, таких как GitHub и GitLab. Представляет собой запрос от разработчика на слияние изменений из одной ветки в другую, часто из форка в исходный проект. После создания PR другие разработчики могут просмотреть, обсудить и, при необходимости, внести комментарии или изменения в предложенные изменения перед их слиянием;
- Индекс (Index) - это промежуточное хранилище, где разработчик помещает измененные файлы перед коммитом. Файлы, добавленные в индекс, готовы к коммиту и будут включены в следующий коммит;
- Тег (Tag) - это ссылка на конкретный коммит, используемая для пометки определенных состояний проекта, таких как релизы или важные моменты в истории проекта. Теги обычно используются для обозначения стабильных версий приложения;
- HEAD - это символическая ссылка на текущий коммит в вашем рабочем каталоге. Он указывает на коммит, с которым вы в данный момент работаете. Когда вы создаете новый коммит, HEAD обновляется, чтобы указывать на этот новый коммит;
- Хеш (Hash) или хеш-сумма - это уникальный идентификатор, который присваивается каждому коммиту, вычисляется на основе содержимого коммита, уникально идентифицирует этот коммит в истории проекта. Хеши используются для ссылки на коммиты и обеспечивают целостность данных.
## Основные команды Git

### Создание репозитория

`git init`: создание нового репозитория в текущей директории, в результате чего создается новая директория .git, где хранится вся информация о репозитории, коммитах, ветках и настройках
`git clone <URL>`: клонирование удаленного репозитория Git в локальную директорию - загружаются все коммиты, ветки и файлы из удаленного репозитория и создается локальная копия проекта

### Внесение изменений

`git status`: вывод измененных или новых файлов, которые в дальнейшем нужно проиндексировать
`git log`: вывод истории коммитов текущей ветки, содержащий хэш коммита, автора, время и сообщение коммита
`git log --oneline`: вариация команды `git log`, которая выводит более краткую историю коммитов, содержащую сокращенный хэш коммита и его сообщение в одной строке
`git diff`: разница между коммитами, ветками или файлами
`git add <file/dir>`: индексация файлы или директория для коммита
`git commit -m "<message name>"`: создание коммита с изменениями, добавленными в индекс

### Работа с ветками

`git branch`: список веток в репозитории
`git branch <branch>`: создание новой ветки
`git checkout <branch>`: переключение между ветками
`git checkout -`: загружает предыдущую ветку, удобно для быстрого переключения
`git stash`: используется для временного сохранения незавершенных изменений, чтобы переключиться на другую ветку или выполнить другие операции без потери работы
`git merge <branch>`: внесение изменения указанной ветки в текущую ветку
`git merge --no-ff <branch>`: внесение изменения указанной ветки в текущую ветку, так, что изменения из указанной ветки просто добавляются к основной ветке без создания дополнительного коммита слияния
`git branch -d <branch>`: удаление указанной ветки
`git rebase <branch>`: переписывание коммитов текущей ветки после коммитов в указанной ветке
`git fetch`: взятие всех изменений из удаленного репозитория и сохранение этих изменений локально
`git pull`: взятие всех изменений из удаленного репозитория и слиянние этих изменений с текущей веткой, работает как комбинация команд `git fetch` и `git merge`
`git push`: устанавливается становление связи с удалённым репозиторием, берутся все отсутствующие изменения удаленного репозитория и далее сохранение этих изменений в удаленный репозиторий

### Merge vs Rebase

Merge и Rebase - это два разных способа интеграции изменений из одной ветки в другую, которые стоит рассмотреть подробнее. Давайте разберемся с этими двумя командами и их особенностями:

#### Merge

Merge - это процесс объединения изменений из одной ветки в другую. При этом создается новый коммит, который объединяет изменения из обеих веток. Вот как выглядит процесс слияния:

1. Переключение на ветку, в которую хотим внести изменения `git checkout main`
2. Выполнение команды `git merge <branch>`, где <branch> - ветка, из которой вы хотите взять изменения.
3. Git попытается объединить изменения из указанной ветки в текущую. Если есть конфликты, Git попросит вас разрешить их вручную. Вы должны решить конфликты, сохранить изменения и сделать коммит, чтобы завершить слияние.

#### Rebase

Rebase - это более продвинутый способ интеграции изменений, который позволяет вам переписать историю коммитов текущей ветки так, как будто вы начали работу с этой веткой после изменений из другой ветки. Вот как это работает:

1. Переключение на ветку, в которую хотим внести изменения `git checkout main`
2. Выполнение команды `git rebase <branch>`, где <branch> - ветка, из которой вы хотите взять изменения.
3. Git возьмет ваши коммиты из текущей ветки и применит их поверх последнего коммита из указанной ветки. Если есть конфликты, вы должны их разрешить, как при слиянии.

Interactive Rebase позволяет контролировать, редактировать историю коммитов и многое другое.

Вы можете использовать команду `git rebase -i HEAD~N`, где N - это количество коммитов, которые вы хотите редактировать.

После запуска этой команды, вы увидите список коммитов в текстовом редакторе, где вы можете выбирать действия для каждого коммита (pick, squash, edit, et al.). Например, чтобы объединить коммиты в один, вы можете заменить pick на squash. После завершения интерактивного ребейза, вы можете использовать git push --force, чтобы отправить измененную историю в удаленный репозиторий.

# GitFlow

GitFlow является одной из наиболее популярных стратегий ветвления и слияния для управления версиями в Git. Он предоставляет структуру для эффективного сотрудничества между разработчиками, управления релизами и поддержкой долгосрочных и краткосрочных фич.

## Branching strategies

Cуществует множество различных стратегий ветвления, которые, разработчики выбирают в зависимости от потребностей и сложности своих проектов. В рамках этого документа рассмотрим стратегию GitFlow.

Основные ветки:
- **main**: стабильные и готовые к выпуску версии проекта, каждый коммит в этих ветках представляет собой новый релиз;
- **develop**: все новые функции и исправления ошибок сначала добавляются в эту ветку перед тем как они попадут в main.

Вспомогательные ветки:
- **feature**: создаются для разработки новых функций;
- **bugfix**: используются для исправления ошибок в коде;
- **hotfix**: используются для быстрого исправления критических ошибок, обнаруженных в релизе, вливается как в main, так и в develop;
- **release**: создаются для подготовки новых версий к релизу, завершается работа над версией, вносятся последние изменения и тестирование перед релизом.

## GitFlow use cases

Рассмотрим несколько end-to-end сценариев, связанных с работой над опенсорсными проектами, и проиллюстрируем их использование с помощью различных Git-команд. 

### Создание/клонирование репозитория

Разработчик хочет создать новый или же склонировать существующий репозиторий проекта.

При создании репозитория создается директория .git внутри директории проекта. Все данные Git, такие как история коммитов и настройки репозитория, хранятся в этой директории.

`git init`

При клонировании репозитория создается копия удаленного репозитория на локальной машине в новой директории с именем репозитория.

`git clone <URL>`

### Создание новой фичи

Разработчик хочет добавить новую фичу (функцию) в проект, для этого нужно создать и перейти в соответственную для этой фичи ветку.

`git checkout develop`

`git checkout feature/new-feature`


### Работа над фичей

Разработчик хочет внести изменения в код ветки фичи, для этого он должен коммитить изменения и пушить их в удаленный репозиторий.

`git add <files>` или `git add .` для добавления всех измененных файлов в индекс.

`git commit -m "feat: add [feature]"`

`git push origin feature/new-feature`


### Завершение работы над фичей и начало ревью

После завершения работы над фичей, разработчик создает Pull Request для интеграции своих изменений в основную ветку.

`git checkout develop`

`git pull origin develop`

Подтягивание последних изменений из основной ветки важно, чтобы ваша ветка фичи не отстала от текущего состояния проекта и чтобы минимизировать возможность конфликтов при слиянии.

`git checkout feature/new-feature`

`git rebase develop`

`git push origin feature/new-feature`

После выполнения этих шагов, вы можете создать Pull Request (PR) на веб-платформе (например, GitHub), чтобы начать процесс ревью ваших изменений другими участниками проекта. Не забудьте описать свои изменения и добавить необходимую информацию для ревьюера, чтобы им было легче понять, что вы сделали и почему.


### Ревью кода и слияние фичи

Другие разработчики рассматривают раннее созданный Pull Request, предлагают изменения и оставляют комментарии. После завершения ревью фича готова к слиянию с основной веткой.

`git checkout develop`

`git pull origin develop`

`git merge --no-ff feature/new-feature`

`git push origin develop`

Если в процессе работы над вашей фичей были изменения в основной ветке, при слиянии Pull Request может возникнуть конфликт. Git попросит вас разрешить этот конфликт, редактируя конфликтные файлы вручную. После разрешения конфликта, сделайте коммит и продолжайте процесс слияния PR.

### Релиз

Для подготовки новый версии проекта создается релизная ветка. Происходит это, когда завершено достаточное количество фич.

`git checkout develop`

`git pull origin develop`

`git checkout release/0.0.1`


### Исправление ошибок в релизе

Если в уже созданном релизе имеются ошибки, разработчики могут исправить их прямо в релизной ветке.

`git commit -m "fix: solved [critical bug]"`

`git push origin release/0.0.1`


### Завершение релиза и создание тега

Когда все ошибки успешно исправлены и релиз готов к выпуску, создается тег. 

`git checkout main`

`git merge --no-ff release/0.0.1`

`git tag -a 0.0.1 -m "Release 0.0.1"`

`git push origin main`

`git push origin --tags`


### Поддержка релиза

Если вдруг после выпуска релиза были обнаружены ошибки, то разработчик может их исправить в той же ветке, закоммитив и внеся изменения.

`git checkout release/0.0.1`

`git commit -a -m "fix: solved [critical post-release bug]"`

`git push origin release/0.0.1`


### Внедрение исправлений в основную ветку

Для того, чтобы внесенные в релизную ветку изменения были доступны в будущем в других релизах, эти изменения могут быть внедрены в основную ветку разработки. Разработчик хочет внести изменения в код ветки фичи, для этого он должен коммитить изменения и пушить их в удаленный репозиторий:

`git checkout develop`

`git pull origin develop`

`git merge --no-ff release/0.0.1`

`git push origin develop`


### Удаление веток

Ненужные ветки, оставшиеся после завершения работы над фичами и релизами могут быть удалены.

`git branch -d feature/new-feature`

`git branch -d release/0.0.1`

`git push origin --delete feature/new-feature`

`git push origin --delete release/0.0.1`

### Удаление файлов

Для удаления файла из индекса и физически из файловой системы можно использовать:

`git rm <file>`

Для удаления файла из индекса, но не физически из файловой системы можно использовать:

`git rm --cached <file>`

### Переход к старому коммиту

Сначала вы должны найти хеш коммита, к которому вы хотите вернуться. Это можно сделать, используя команду `git log`, чтобы просмотреть историю коммитов и скопировать хеш нужного коммита. Далее на базе этого хеша коммита можно создать новую ветку, и делать с ней то, что уже рассматривалось: вносить изменения, объеденять изменения с другими ветками.

`git checkout -b <new_branch> <hash>`

 Если вам нужно вернуться к предыдущему состоянию, вы можете сделать это, переключившись обратно на другую ветку.

 `git checkout -b <branch>`

 ### Отмена предыдущего коммита

 Для отмены предыдущих коммитов, создаются новые коммиты, которые отменяют изменения предыдущих коммитов.

 `git revert <hash>`
