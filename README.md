## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
# Открыть сайт по URL
$ open https://git-scm.com
```

## Tasks

- [X] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [X] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [X] 3. Ознакомиться со ссылками учебного материала
- [X] 4. Выполнить инструкцию учебного материала
- [X] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

Присваивание значений глобальным параметрам
```ShellSession
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенирированный_токен>
$ alias edit=<nano|vi|vim|subl>
```

Активация скрипта
```ShellSession
$ cd ${GITHUB_USERNAME}/workspace
$ source scripts/activate

```

```ShellSession
# Создаем директорию в корневой папке, конфигурируем hub
$ mkdir ~/.config
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF

# Устанавливаем переменную git 
$ git config --global hub.protocol https
```

Редактирование репозитория
```ShellSession
# Создание и переход в директорию
$ mkdir projects/lab02 && cd projects/lab02

# Создаем пустой/инициализируем существующий Git-репозиторий.
$ git init
# Initialized empty Git repository in /home/momhustler/bootyass/workspace/projects/lab02/.git/

# Устанавливаем глобальные параметры для git
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}

# Вывод всего конфига
$ git config -e --global
[user]
        email = panda_canniball@mail.ru
        name = BootyAss
[hub]
        protocol = https


# Добавляем ссылку на репозиторий
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git

# Получаем изменения с github
$ git pull origin master
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Распаковка объектов: 100% (3/3), done.
Из https://github.com/BootyAss/lab02
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> origin/master

# Создаем файл README.md
$ touch README.md

# Выводим статус репозитория
$ git status
На ветке master
нечего коммитить, нет изменений в рабочем каталоге

# Добавляем README.md
$ git add README.md

# Создаем коммит 
$ git commit -m"added README.md"
[master 6a45a1d] added sources
 1 file changed, 4 insertions(+)
 create mode 100644 README.md
 
# Отправляем изменения в репозиторий
$ git push origin master
Перечисление объектов: 1, готово.
Подсчет объектов: 100% (1/1), готово.
При сжатии изменений используется до 12 потоков
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (2/2), 10 bytes | 850.00 KiB/s, готово.
Всего 2 (изменения 0), повторно использовано 0 (изменения 0)
To https://github.com/BootyAss/lab02.git
   28640e6..6a45a1d  master -> master

```
Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

Содержание ".gitignore"
```ShellSession
*build*/
*install*/
*.swp
.idea/
```

Проверка изменений 
```ShellSession
# Получаем изменения
$ git pull origin master
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Распаковка объектов: 100% (3/3), done.
Из https://github.com/BootyAss/lab02
 * branch            master     -> FETCH_HEAD
   44830ab..c52a23e  master     -> origin/master
Fast-forward
 .gitignore | 4 ++++
 1 file changed, 4 insertions(+)
 create mode 100644 .gitignore

# Выводим все коммиты 
$ git log
```

Добавление файлов
```ShellSession
# Создаем 3 папки
$ mkdir sources
$ mkdir include
$ mkdir examples

№ Создаем .cpp файл в sources
$ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
```

```ShellSession
# Создаем .hpp файл в include
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```ShellSession
# Создаем .cpp файл в examlpes
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```ShellSession
# Создаем .cpp файл в examlpes
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

Редактирование файла README
```ShellSession
$ edit README.md
```


```ShellSession
$ git status
На ветке master
Неотслеживаемые файлы:
  (используйте «git add <файл>…», чтобы добавить в то, что будет включено в коммит)

        examples/
        include/
        sources/

ничего не добавлено в коммит, но есть неотслеживаемые файлы (используйте «git add», чтобы отслеживать их)

$ git add .

# Фиксация всех изменений
$ git commit -m"added sources"
[master 6a45a1d] added sources
 4 files changed, 32 insertions(+)
 create mode 100644 examples/example1.cpp
 create mode 100644 examples/example2.cpp
 create mode 100644 include/print.hpp
 create mode 100644 sources/print.cpp

# Отправляем изменения в репозиторий
$ git push origin master
Перечисление объектов: 10, готово.
Подсчет объектов: 100% (10/10), готово.
При сжатии изменений используется до 12 потоков
Сжатие объектов: 100% (7/7), готово.
Запись объектов: 100% (9/9), 930 bytes | 930.00 KiB/s, готово.
Всего 9 (изменения 0), повторно использовано 0 (изменения 0)
To https://github.com/BootyAss/lab02.git
   28640e6..6a45a1d  master -> master

```

## Report

Переносим файлы в репозиторий GIThub
```ShellSession
$ cd ~/workspace/labs/
$ export LAB_NUMBER=02

# Клонируем репозиторий в новую директорию
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}

# Копируем файлы
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
# Not working # command not found
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
4. Добавьте этот файл в локальную копию репозитория.
5. Закоммитьте изменения с *осмысленным* сообщением.
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
8. Запуште изменения в удалёный репозиторий.
9. Проверьте, что история коммитов доступна в удалёный репозитории.

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
3. **commit**, **push** локальную ветку в удалённый репозиторий.
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
5. Создайте pull-request `patch1 -> master`.
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
7. **commit**, **push**.
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
10. Локально выполните **pull**.
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
12. Удалите локальную ветку `patch1`.

### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
5. Убедитесь, что в pull-request появились *конфликтны*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
7. Сделайте *force push* в ветку `patch2`
8. Убедитель, что в pull-request пропали конфликтны. 
9. Вмержите pull-request `patch2 -> master`.

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2019 The ISC Authors
```
