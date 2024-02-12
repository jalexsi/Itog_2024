# Инструкция для работы с git и удаленными репозиториями

## Что такое git?
Git — это распределенная система управления версиями, которая означает, что локальный клон проекта — это полный репозиторий управления версиями. Полнофункциональные локальные репозитории упрощают работу как в автономном, так и в удаленном режиме. Разработчики фиксируют свою работу локально, а затем синхронизируют копию репозитория с копией на сервере.

## Подготовка репозитория
 $ git init
 Эта команда создаёт в текущем каталоге новый подкаталог с именем .git, содержащий все необходимые файлы репозитория — структуру Git репозитория. На этом этапе ваш проект ещё не находится под версионным контролем. Подробное описание файлов, содержащихся в только что созданном вами каталоге .git, приведено в главе Git изнутри

 Если вы хотите добавить под версионный контроль существующие файлы (в отличие от пустого каталога), вам стоит добавить их в индекс и осуществить первый коммит изменений. Добиться этого вы сможете запустив команду git add несколько раз, указав индексируемые файлы, а затем выполнив git commit:

 $ git add *.c
 $ git add LICENSE
 $ git commit -m 'Initial project version'
 Мы разберем, что делают эти команды чуть позже. Теперь у вас есть Git-репозиторий с отслеживаемыми файлами и начальным коммитом.

## Создание коммитов
 git commit [-a | --interactive | --patch] [-s] [-v] [-u<режим>] [--изменить]
 [--предварительный запуск] [(-c | -C | --squash) <фиксация> | --исправление [(изменить | переформулировать):]<фиксация>)]
 [-F <файл> | -m <сообщение>] [--reset-author] [--allow-пустой]
 [--allow-empty-message] [--no-verify] [-e] [--author=<автор>]
 [--date=<дата>] [--очистка=<режим>] [--[нет-] статуса]
 [-ввод -вывод] [--pathspec-from-file=<файл> [--pathspec-file-nul]]
 [(--trailer <токен>[(=|:)<значение>])...] [-S[<keyid>]]
 [--] [<спецификация пути>...]
 Описание
 Создайте новый коммит, содержащий текущее содержимое индекса и заданное сообщение журнала с описанием изменений. Новый коммит является прямым дочерним элементом HEAD, обычно это вершина текущей ветви, и ветвь обновляется, указывая на нее (если только ни одна ветвь не связана с рабочим деревом, и в этом случае HEAD "отсоединяется", как описано в git-checkout[1]).

## Git add
 git-add - добавить содержимое файла в индекс

 КРАТКИЙ обзор
 git add [--verbose | -v] [--dry-run | -n] [--force | -f] [--interactive | -i] [--patch | -p]
 [--edit | -e] [--[no-]all | -A | --[no-]игнорировать удаление | [--update | -u]] [--sparse]
 [--намерение добавить | -N] [--обновить] [--игнорировать-ошибки] [--игнорировать-отсутствует] [--перенормировать]
 [--chmod=(+|-)x] [--pathspec-from-file=<файл> [--pathspec-file-nul]]
 [--] [<спецификация пути>...]
 Описание
 Эта команда обновляет индекс, используя текущее содержимое, найденное в рабочем дереве, чтобы подготовить содержимое для следующего коммита. Обычно он добавляет текущее содержимое существующих путей в целом, но с некоторыми опциями его также можно использовать для добавления содержимого с применением только части изменений, внесенных в файлы рабочего дерева, или удаления путей, которые больше не существуют в рабочем дереве.

 "Индекс" содержит снимок содержимого рабочего дерева, и именно этот снимок берется в качестве содержимого следующего коммита. Таким образом, после внесения любых изменений в рабочее дерево и перед выполнением команды фиксации вы должны использовать команду add для добавления любых новых или измененных файлов в индекс.

 Эта команда может быть выполнена несколько раз перед фиксацией. Он добавляет содержимое только указанных файлов во время выполнения команды add ; если вы хотите, чтобы последующие изменения были включены в следующий коммит, вам необходимо выполнить git add еще раз, чтобы добавить новое содержимое в индекс.

 Команда git status может использоваться для получения сводной информации о том, в какие файлы внесены изменения, подготовленные для следующего коммита.

 Команда git add по умолчанию не добавляет игнорируемые файлы. Если какие-либо игнорируемые файлы были явно указаны в командной строке, git add завершится ошибкой со списком игнорируемых файлов. Игнорируемые файлы, полученные в результате рекурсии каталога или изменения имени файла, выполняемого Git (укажите ваши глобусы перед командной строкой), будут автоматически проигнорированы. Команда git add может использоваться для добавления игнорируемых файлов с помощью -f опции (принудительно).

 Пожалуйста, ознакомьтесь с git-commit[1], чтобы узнать об альтернативных  способах добавления содержимого в коммит.


### Просмотр состояния репозитория
  git-status - показывает состояние рабочего дерева

 КРАТКИЙ обзор
 состояние git [<параметры>] [--] [<спецификация пути>...]
 Описание
 Отображает пути, которые имеют различия между индексным файлом и текущим заголовочным коммитом, пути, которые имеют различия между рабочим деревом и индексным файлом, и пути в рабочем дереве, которые не отслеживаются Git (и не игнорируются gitignore[5]). Первые - это то, что вы бы зафиксировали при запуске git commit; вторые и третьи - это то, что вы могли бы зафиксировать, запустив git add перед запуском git commit

### Просмотр удаленных репозиториев
 Работа с удалёнными репозиториями
 Для того, чтобы внести вклад в какой-либо Git-проект, вам необходимо уметь работать с удалёнными репозиториями. Удалённые репозитории представляют собой версии вашего проекта, сохранённые в интернете или ещё где-то в сети. У вас может быть несколько удалённых репозиториев, каждый из которых может быть доступен для чтения или для чтения-записи. Взаимодействие с другими пользователями предполагает управление удалёнными репозиториями, а также отправку и получение данных из них. Управление репозиториями включает в себя как умение добавлять новые, так и умение удалять устаревшие репозитории, а также умение управлять различными удалёнными ветками, объявлять их отслеживаемыми или нет и так далее. В данном разделе мы рассмотрим некоторые из этих навыков.
 Просмотр удалённых репозиториев
 Просмотр удалённых репозиториев
 Для того, чтобы просмотреть список настроенных удалённых репозиториев, вы можете запустить команду git remote. Она выведет названия доступных удалённых репозиториев. Если вы клонировали репозиторий, то увидите как минимум origin — имя по умолчанию, которое Git даёт серверу, с которого производилось клонирование:

 $ git clone https://github.com/schacon/ticgit
 Cloning into 'ticgit'...
 remote: Reusing existing pack: 1857, done.
 remote: Total 1857 (delta 0), reused 0 (delta 0)
 Receiving objects: 100% (1857/1857), 374.35 KiB | 268.00 KiB/s, done.
 Resolving deltas: 100% (772/772), done.
 Checking connectivity... done.
 $ cd ticgit
 $ git remote
 origin
 Вы можете также указать ключ -v, чтобы просмотреть адреса для чтения и записи, привязанные к репозиторию:

 $ git remote -v
 origin	https://github.com/schacon/ticgit (fetch)
 origin	https://github.com/schacon/ticgit (push)

### Добавление удалённых репозиториев
 Добавление удалённых репозиториев
 В предыдущих разделах мы уже упоминали и приводили примеры добавления удалённых репозиториев, сейчас рассмотрим эту операцию подробнее. Для того, чтобы добавить удалённый репозиторий и присвоить ему имя (shortname), просто выполните команду git remote add <shortname> <url>:

 $ git remote
 origin
 $ git remote add pb https://github.com/paulboone/ticgit
 $ git remote -v
 origin	https://github.com/schacon/ticgit (fetch)
 origin	https://github.com/schacon/ticgit (push)
 pb	https://github.com/paulboone/ticgit (fetch)
 pb	https://github.com/paulboone/ticgit (push)

 
