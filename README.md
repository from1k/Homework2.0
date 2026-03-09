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

#### Пункты 1 и 2. Выполним в соответствии с командами, указанными в [Tutorial](https://github.com/tp-labs/lab02) и создадим пустой репозиторий, в котором будет происходит дальнейшая работа.

> *Примечание: первый commit через терминал был реализован на основе сырого файла hello_world.cpp, который создвется после первого commit'а в лабораторной  работе. Проблем это вызвать не должно, они бы появились, если бы в проекте не было commit'ов в целом. Initial commit'ом в [репозитории](https://github.com/from1k/Homework2/tree/main) является файл LICENSE* 
 
#### Пункт 3. Создайте файл hello_world.cpp в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу Hello world на языке C++ используя плохой стиль кода.

+ Реализация:  
```bash
$ cd Homework2
$ nano hello_world
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

+ Реализация:
  
```bash
$ git add hallo_world.cpp
$ git commit -m "create hello_world.cpp (raw version)"
```
+ Терминал:
  
```bash
[main e04ac07] create hello_world.cpp (raw version)
 1 file changed, 7 insertions(+)
 create mode 100644 hello_world.cpp
```
#### Пункты 6 и 7. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивала имя пользователя. А в стандартный поток вывода печаталось сообщение Hello world from @name, где @name имя пользователя.

+ Реализация:
  
```bash
$ nano hallo_world.cpp
$ git commit -am "added user input"
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
+ Терминал:
  
```bash
[main 6720bcf] added user input
 1 file changed, 7 insertions(+), 2 deletions(-)
```
> *Примечание: нужно ли использовать ```git add``` повторно? Нет, ведь файл hello_world.cpp уже был добавлен ранее и Git его отслеживает. Поэтому Git знает, что этот файл изменился, и включит его в commit.*

#### Пункт 8. Запуште изменения в удалёный репозиторий.

+ Реализация:
  
```bash
$ git push -u origin main
```
+ Терминал:
  
```bash
[main 6720bcf] added user input
Username for 'https://github.com': ${GITHUB_USERNAME}
Password for 'https://from1k@github.com': 
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 3 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 772 bytes | 772.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/from1k/Homework2
   5d377d4..6720bcf  main -> main
branch 'main' set up to track 'origin/main'.
```
#### Пункт 9. Проверьте, что история коммитов доступна в удалёный репозитории.

+ Реализация:
  
```bash
$ git log --oneline
```
+ Терминал:
  
```bash
6720bcf (HEAD -> main, origin/main, origin/HEAD) added user input
e04ac07 create hello_world.cpp (raw version)
5d377d4 Initial commit
```
### Часть 2

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

#### Пункты 6 и 7. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивала имя пользователя. А в стандартный поток вывода печаталось сообщение Hello world from @name, где @name имя пользователя.

+ Реализация:
  
```bash
$ nano hallo_world.cpp
$ git commit -am "added user input"
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
+ Терминал:
  
```bash
[main 6720bcf] added user input
 1 file changed, 7 insertions(+), 2 deletions(-)
```
> *Примечание: нужно ли использовать ```git add``` повторно? Нет, ведь файл hello_world.cpp уже был добавлен ранее и Git его отслеживает. Поэтому Git знает, что этот файл изменился, и включит его в commit.*

#### Пункт 8. Запуште изменения в удалёный репозиторий.

+ Реализация:
  
```bash
$ git push -u origin main
```
+ Терминал:
  
```bash
[main 6720bcf] added user input
Username for 'https://github.com': from1k
Password for 'https://from1k@github.com': 
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 3 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 772 bytes | 772.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/from1k/Homework2
   5d377d4..6720bcf  main -> main
branch 'main' set up to track 'origin/main'.
```
#### Пункт 9. Проверьте, что история коммитов доступна в удалёный репозитории.

+ Реализация:
  
```bash
$ git log --oneline
```
+ Терминал:
  
```bash
6720bcf (HEAD -> main, origin/main, origin/HEAD) added user input
e04ac07 create hello_world.cpp (raw version)
5d377d4 Initial commit
```

</details>
