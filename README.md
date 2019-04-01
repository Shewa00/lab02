## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [X] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [X] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [X] 3. Ознакомиться со ссылками учебного материала
- [X] 4. Выполнить инструкцию учебного материала
- [x] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```ShellSession
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенирированный_токен>
$ alias edit=<nano|vi|vim|subl>

```

```ShellSession
$ cd ${GITHUB_USERNAME}/workspace
$ source scripts/activate #активация скрипта
```

```ShellSession
$ mkdir ~/.config #создаем папку с конфигом
$ cat > ~/.config/hub <<EOF #создаем файл hub и записываем в него 
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https #Устанавливаем параметр конфига гит
```

```ShellSession
$ mkdir projects/lab02 && cd projects/lab02
$ git init
Initialized empty Git repository in /Users/macbook/Shewa00/workspace/.git/
$ git config --global user.name ${GITHUB_USERNAME} # Установка параметра конфига username для git
$ git config --global user.email ${GITHUB_EMAIL} # Установка параметра конфига email для git
# check your git global settings
$ git config -e --global #вывод конфига
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git # добавление ссылки на репозиторий гитхаба
$ git pull origin master #переносим изменения с гитхаба
$ touch README.md #создаем README.md
$ git status #узнаем статус репозитория
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	node/
	reports/
	scripts/
	tasks/

nothing added to commit but untracked files present (use "git add" to track)

$ git add README.md #добавляем файл
$ git commit -m"added README.md" #закомитить изменения 
On branch master
Untracked files:
	node/
	reports/
	scripts/
	tasks/

nothing added to commit but untracked files present
$ git push origin master
```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```ShellSession
*build*/
*install*/
*.swp
.idea/
```

```ShellSession
$ git pull origin master
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 2
Unpacking objects: 100% (3/3), done.
From https://github.com/Shewa00/lab02
 * branch            master     -> FETCH_HEAD
   7370432..ea3ca1f  master     -> origin/master
Updating 7370432..ea3ca1f
Fast-forward
 .gitignore | 4 ++++
 1 file changed, 4 insertions(+)
 create mode 100644 .gitignore
$ git log
commit ea3ca1fcb804f2f73b382de0e2adb1a63dc6775d (HEAD -> master, origin/master)
Author: Shewa00 <47750099+Shewa00@users.noreply.github.com>
Date:   Mon Apr 1 17:56:56 2019 +0300

    Create .gitignore

commit 7370432f9c661d97a72c36d35d4c346b11159184
Merge: ed14855 36da062
Author: rusdevops <rusdevops@gmail.com>
Date:   Thu Feb 28 17:24:16 2019 +0300

    Merge pull request #1 from drewxa/patch-1
    
    added homework

commit 36da062d807b544e0af524275c3c79e73320f2b0
Author: drewxa <bo.ro.da@mail.ru>
Date:   Tue Feb 26 19:48:32 2019 +0300

    added homework
    
    Добавлено задания для самоподготовки:
    * init
    * commit
    * log
    * push
    * rebase

commit ed14855954e0f21b177e3e7e541eb763b86dd674
Author: rusdevops <rusdevops@gmail.com>
Date:   Sun Jan 20 11:28:59 2019 +0000

    fixed lab ID

commit 457bbf6275564245978ae511ed8aea53cda81de5
Author: rusdevops <rusdevops@gmail.com>
Date:   Sun Jan 20 11:25:58 2019 +0000

    move hub installation to lab00

commit 2565c654e3cf8322c6e7b02210cfbb04d25ba2e3
Author: rusdevops <rusdevops@gmail.com>
Date:   Sun Jan 20 13:29:16 2019 +0300

    Update README.md

commit 3e78c8c11ae5fba16a7e74e11b495c6584e018f7
Author: rusdevops <rusdevops@gmail.com>
Date:   Sun Jan 20 13:26:47 2019 +0300

    Update README.md

commit 4e04eb75d8c2f607770c264631910fdbe33c650c
Author: rusdevops <rusdevops@gmail.com>
Date:   Sun Jan 20 13:05:32 2019 +0300

    Update README.md

commit 82e7b76a958b4609b76804f0303cf5780c0d6d3b
Author: rusdevops <rusdevops@gmail.com>
Date:   Thu Oct 26 19:00:56 2017 -0800
refactored
...

commit a968e67febbb7cca46125868032c5f785a445f81
Author: rusdevops <rusdevops@gmail.com>
Date:   Thu Apr 27 14:45:43 2017 +0300

    Create README.md

commit 550513f0218a8737ebbc17d40135afae4155b674
Author: rusdevops <rusdevops@gmail.com>
Date:   Thu Apr 27 14:44:04 2017 +0300
 Initial commit

```

```ShellSession
$ mkdir sources
$ mkdir include
$ mkdir examples
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
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```ShellSession
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```ShellSession
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

```ShellSession
$ edit README.md
```

```ShellSession
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	examples/
	include/
	node/
	reports/
	scripts/
	sources/
	tasks/

nothing added to commit but untracked files present (use "git add" to track)
MacBook-Pro-Igor:workspace macbook$ 

$ git add .
warning: adding embedded git repository: reports/lab01
hint: You've added another git repository inside your current repository.
hint: Clones of the outer repository will not contain the contents of
hint: the embedded repository and will not know how to obtain it.
hint: If you meant to add a submodule, use:
hint: 
hint: 	git submodule add <url> reports/lab01
hint: 
hint: If you added this path by mistake, you can remove it from the
hint: index with:
hint: 
hint: 	git rm --cached reports/lab01
hint: 
hint: See "git help submodule" for more information.
warning: adding embedded git repository: tasks/lab01

$ git commit -m"added sources"

[master 60240af] added sources
 4101 files changed, 546262 insertions(+)
 create mode 100644 examples/example1.cpp
 create mode 100644 examples/example2.cpp
 create mode 100644 include/print.hpp
 create mode 100644 node/CHANGELOG.md
 .....
 create mode 160000 reports/lab01
 create mode 100644 scripts/activate
 create mode 100644 sources/print.cpp
 create mode 160000 tasks/lab01

$ git push origin master
Enumerating objects: 4215, done.
Counting objects: 100% (4215/4215), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4027/4027), done.
Writing objects: 100% (4214/4214), 16.94 MiB | 148.00 KiB/s, done.
Total 4214 (delta 688), reused 0 (delta 0)
remote: Resolving deltas: 100% (688/688), done.
To https://github.com/Shewa00/lab02.git
   ea3ca1f..60240af  master -> master
```

## Report

```ShellSession
$ cd ~/workspace/labs/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
Initialized empty Git repository in /Users/macbook/Shewa00/workspace/reports/lab02/.git/
[master (root-commit) 4c55294] Initial gistup commit.
 1 file changed, 205 insertions(+)
 create mode 100644 REPORT.md
/Users/macbook/Shewa00/workspace/node/lib/node_modules/gistup/lib/gistup/unless.js:11
    throw error;
    ^

Error: invalid gist id: undefined
    at /Users/macbook/Shewa00/workspace/node/lib/node_modules/gistup/bin/gistup:169:67
    at IncomingMessage.<anonymous> (/Users/macbook/Shewa00/workspace/node/lib/node_modules/gistup/lib/gistup/api.js:28:7)
    at IncomingMessage.emit (events.js:202:15)
    at endReadableNT (_stream_readable.js:1129:12)
    at processTicksAndRejections (internal/process/next_tick.js:76:17)
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
