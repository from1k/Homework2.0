# Homework2.0
Выполнение лабораторной работы, посвещенной изучению систем контроля версий на примере Git.
## Теоретическая часть
<details>
<summary> Нажмите, чтобы раскрыть </summary>  
  
### Основные понятия Git
+ commit — сохранение изменений в репозитории с описанием;
+ branch (ветка) — независимая линия разработки, которая позволяют работать над новыми функциями, не затрагивая основную версию;
+ merge — процесс объединения (слияния) изменений из одной ветки в другую;
+ pull-request — механизм предложения изменений для включения их в основную ветку проекта;
+ rebase — операция перемещения или переписывания истории коммитов для более линейной истории разработки;
+ merge conflict — конфликт, при котором Git не может автоматически объединить изменения из разных веток.

### Работа с изменениями
+ ```git clone``` rопирует удалённый репозиторий на локальный компьютер;
+ ```git init``` создает новый локальный репозиторий;
+ ```git config``` используется для настройки параметров Git.
    
### Работа с изменениями
+ ```git add``` добавляет новые изменения;
+ ```git commit``` сохраняет изменения в истории репозитория.

### Работа с удаленным репозиторием
+ ```git commit``` отправляет локальные изменения в удаленный репозиторий;
+ ```git pull```  получает изменения из удаленнго репозитория и объединяет их м локальной веткой;
+ ```git fetch``` получает изменения из удалённого репозитория без автоматического объединения;
+ ```git remote``` используется для управления ссылками на удаленные репозитории.

### Работа с ветками
+ ```git branch``` показывает список веток или создаёт новую ветку;
+ ```git checkout``` переключается на другую ветку;
+ ```git checkout -b <branch>``` создаёт новую ветку и сразу переключается на неё.

### Слияние и переписывание истории
+ ```git merge``` объединяет изменения из одной ветки в другую;
+ ```git rebase``` переносит коммиты текущей ветки на другую ветку.
+ ```git rebase --continue``` продолжает процесс rebase.

### Работа с конфликтами
+ ```git status``` показывает состояние репозитория и наличие конфликтов.
  </details>

## Практическая часть
<details>
<summary> Нажмите, чтобы раскрыть </summary>  

### Часть 1
<details>
<summary> Нажмите, чтобы раскрыть </summary>  

#### Пункты 1 и 2. Выполним в соответствии с командами, указанными в [Tutorial](https://github.com/tp-labs/lab02) и создадим пустой [репозиторий](https://github.com/from1k/GitExample), в котором будет происходит дальнейшая работа.

+ Реализация + bash:  
```bash
$ mkdir GitExample
$ cd GitExample
$ git init

hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint:  git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint:  git branch -m <name>
Initialized empty Git repository in /home/from1k/from1k/workspace/GitExample/.git/

$ echo "# GitExample" > README.md
$ git add README.md
$ git commit -m "Initial commit"

[master (root-commit) 6d7e0fd] Initial commit
 1 file changed, 1 insertion(+)
 create mode 100644 README.md

$ git remote add origin https://github.com/from1k/GitExample.git
$ git status

On branch master
nothing to commit, working tree clean
from1k@from1k-VirtualBox:~/from1k/workspace/GitExample$ git log
commit 6d7e0fdab97beef98f23e9d907cd042652b2b86d (HEAD -> master)
Author: from1k <ashubin2007@gmail.com>
Date:   Tue Mar 10 10:50:16 2026 +0300

    Initial commit

$ git push -u origin master
Username for 'https://github.com': from1k
Password for 'https://from1k@github.com': 
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 225 bytes | 225.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/from1k/GitExample.git
 * [new branch]      master -> master
branch 'master' set up to track 'origin/master'.
```

#### Пункт 3. Создайте файл hello_world.cpp в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу Hello world на языке C++ используя плохой стиль кода.

+ Реализация + bash:  
```bash
$ nano hello_world.cpp
```

+ Содержимое hello_world.cpp:
```c
#include <iostream>
using namespace std;

int main()
{
  cout << "Hello world" << endl;
  return 0;
}
```

#### Пункты 4 и 5. Добавьте этот файл в локальную копию репозитория. Закоммитьте изменения с осмысленным сообщением.

+ Реализация + bash:
  
```bash
$ git add hello_world.cpp
$ git commit -m "hello_world.cpp created"

[master c131ca9] hello_world.cpp created
 1 file changed, 8 insertions(+)
 create mode 100644 hello_world.cpp
```

#### Пункты 6 и 7. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивала имя пользователя. А в стандартный поток вывода печаталось сообщение Hello world from @name, где @name имя пользователя.

+ Реализация + bash:
  
```bash
$ nano hello_world.cpp
$ git add hello_world.cpp
$ git commit -m "added print username"

[master 42024e7] added print username
 1 file changed, 7 insertions(+), 2 deletions(-)
```
+ Содержимое hello_world.cpp:
```c
#include <iostream>
#include <string>
using namespace std;

int main()
{
  string name;
  cout << "Enter your name: ";
  cin >> name;
  cout << "Hello world from " << name << endl; 
  return 0;
}
```
> *Примечание: нужно ли использовать ```git add``` повторно? Нет, ведь файл hello_world.cpp уже был добавлен ранее и Git его отслеживает. Поэтому Git знает, что этот файл изменился, и включит его в commit.*

#### Пункт 8. Запуште изменения в удалёный репозиторий.

+ Реализация + bash:
  
```bash
$ git push origin master

Username for 'https://github.com': from1k
Password for 'https://from1k@github.com': 
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 3 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 759 bytes | 759.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/from1k/GitExample.git
   6d7e0fd..42024e7  master -> master
```

#### Пункт 9. Проверьте, что история коммитов доступна в удалённом репозитории.

+ Реализация + bash:
  
```bash
$ git log

commit 42024e7be86e0e18aef8b34436feb77402c95f97 (HEAD -> master, origin/master)
Author: from1k <ashubin2007@gmail.com>
Date:   Tue Mar 10 11:04:41 2026 +0300

    added print username

commit c131ca984a8a895fb02eeb4bda746c4c30dc637e
Author: from1k <ashubin2007@gmail.com>
Date:   Tue Mar 10 10:58:06 2026 +0300

    hello_world.cpp created

commit 6d7e0fdab97beef98f23e9d907cd042652b2b86d
Author: from1k <ashubin2007@gmail.com>
Date:   Tue Mar 10 10:50:16 2026 +0300

    Initial commit
```
</details>

### Часть 2
<details>
<summary> Нажмите, чтобы раскрыть </summary>
  
#### Пункт 1. В локальной копии репозитория создайте локальную ветку patch1.

+ Реализация:
  
```bash
$ git checkout -b patch1
```
+ Терминал:
  
```bash
Switched to a new branch 'patch1'
```
> *Примечание: ключ ```-b``` используется для того, чтобы сразу при создании новой ветки переключиться на нее.*
 
#### Пункт 2. Внесите изменения в ветке patch1 по исправлению кода и избавления от using namespace std.

+ Реализация:  
```bash
$ nano hello_world.cpp
```

+ Содержимое hello_world.cpp:
```c
#include <iostream>
#include <string>

int main()
{
  std::string name;
  std::cout << "Enter your name: ";
  std::cin >> name;
  std::cout << "Hello world from " << name << std::endl; 
  return 0;
}
```
#### Пункт 3. Выполняем commit, push локальную ветку в удалённый репозиторий.

+ Реализация + вывод терминала:
  
```bash
$ git commit -am "delete using namespace std"
[patch1 f3b1ab8] delete using namespace std
 1 file changed, 4 insertions(+), 6 deletions(-)
$ git push -u origin patch1
Username for 'https://github.com': ${GITHUB_USERNAME}
Password for 'https://from1k@github.com': 
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 3 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 413 bytes | 413.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'patch1' on GitHub by visiting:
remote:      https://github.com/from1k/Homework2/pull/new/patch1
remote: 
To https://github.com/from1k/Homework2
 * [new branch]      patch1 -> patch1
branch 'patch1' set up to track 'origin/patch1'.
```

#### Пункт 4. Проверьте, что ветка patch1 доступна в удалённом репозитории.

+ Реализация:
  
```bash
$ git branch -r
```
> *Примечание: в списке должно находиться ```origin/pathc1```*

#### Пункт 5. Создайте pull-request patch1 -> master.

+ Реализация + вывод терминала:
  
```bash
$ hub pull-request -b main -h patch1 -m "PR patch1 == main"
https://github.com/from1k/Homework2/pull/1
```
По [ссылке](https://github.com/from1k/Homework2/pull/1) будет создан pull -equest.

> *Примечание: перед выполнением указанной команды необходимо выполнить установку дополнительных модулей с помощью ```sudo apt install hub```*

#### Пункты 6 и 7. В локальной копии в ветке patch1 добавьте в исходный код комментарии + commit, push.

+ Реализация + часть вывода терминала:  
```bash
$ nano hello_world.cpp
$ git commit -am "added comment"
[patch1 71656ee] added comment
 1 file changed, 1 insertion(+)
$ git push
```

+ Содержимое hello_world.cpp:
```c
#include <iostream>
#include <string>

//Programm asks username and print message
int main()
{
  std::string name;
  std::cout << "Enter your name: ";
  std::cin >> name;
  std::cout << "Hello world from " << name << std::endl; 
  return 0;
}
```
+ Терминал:
```bash
Username for 'https://github.com': ${GITHUB_USERNAME}
Password for 'https://from1k@github.com': 
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 3 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 350 bytes | 350.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/from1k/Homework2
   f3b1ab8..71656ee  patch1 -> patch1
```

#### Пункты 8. Проверьте, что новые изменения есть в pull-request.

+ Реализация + вывод терминала:  
```bash
$ git status
On branch patch1
Your branch is up to date with 'origin/patch1'.
```
> *Примечание: ```Your branch is up to date with 'origin/patch1'``` означает, что все изменения отправлены на удаленный репозиторий.*

#### Пункт 9. В удалённый репозитории выполните слияние PR patch1 -> master и удалите ветку patch1 в удаленном репозитории.

+ Реализация + вывода терминала (покомандно):  
```bash
$ git checkout main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

$ git merge patch1
Updating 6720bcf..71656ee
Fast-forward
 hello_world.cpp | 11 +++++------
 1 file changed, 5 insertions(+), 6 deletions(-)

$ git push
Username for 'https://github.com': from1k
Password for 'https://from1k@github.com': 
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/from1k/Homework2
   6720bcf..71656ee  main -> main

$ git branch -d patch1
Deleted branch patch1 (was 71656ee).

$ git log --oneline --graph
* 40f677d (HEAD -> main, origin/main, origin/HEAD) comment was changed
* 71656ee (origin/patch1, patch1) added comment
* f3b1ab8 delete using namespace std
* 6720bcf added user input
* e04ac07 create hello_world.cpp (raw version)
* 5d377d4 Initial commit
```
> *Примечание: вывод команды ```git log --oneline --graph``` возможно был поврежден при копировании. Прошу прощения.*

#### Пункт 10. Локально выполните pull.

+ Реализация:  
```bash
$ git pull origin main
```

+ Терминал:
```bash
Username for 'https://github.com': from1k
Password for 'https://from1k@github.com': 
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), done.
From https://github.com/from1k/Homework2
   71656ee..40f677d  main       -> origin/main
Updating 71656ee..40f677d
Fast-forward
 hello_world.cpp | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

</details>

</details>
