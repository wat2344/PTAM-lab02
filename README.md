# PTAM-lab02
# Laboratory work II

Данная лабораторная работа посвящена изучению систем контроля версий на примере Git.

$ open https://git-scm.com

## Tasks

1. Создать публичный репозиторий с названием lab02 и с лицензией MIT  
   Репозиторий создан.

2. Сгенерировать токен для доступа к сервису GitHub с правами repo  
   Токен создан.

3. Ознакомиться со ссылками учебного материала  
   Ознакомился.

4. Выполнить инструкцию учебного материала.

5. Составить отчет и отправить ссылку личным сообщением в Slack.

## Tutorial

```bash
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенерированный_токен>
```

Это выполнено.

```bash
$ cd ${GITHUB_USERNAME}/workspace
$ source scripts/activate
```

Это тоже выполнено.

```bash
$ mkdir ~/.config
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https
```

Выполнено, файл создан.

```bash
$ mkdir projects/lab02 && cd projects/lab02
$ git init
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
$ git config -e --global
```

Открылся файл, там показаны указанные выше имя и почта.

```bash
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
$ git pull origin master
$ touch README.md
$ git status
$ git add README.md
$ git commit -m"added README.md"
$ git push origin master
```

Дальше на GitHub был создан файл `.gitignore` с содержимым:

```
*build*/
*install*/
*.swp
.idea/
```

```bash
$ git pull origin master
$ git log

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

Файл создан.

```bash
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

Файл создан.

```bash
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

Файл создан.

```bash
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

Файл создан.

```
$ edit README.md
```

Не понял, зачем нужна эта строчка, если мы в файл ничего не записываем.

```bash
$ git status
$ git add .
$ git commit -m"added sources"
$ git push origin master
```

Всё. Выполнил также `compare & pull`, так как у меня была основная ветка `main` с `.gitignore` в ней и созданная ветка `master`. Получил 3 папки с файлами и файл `.gitignore`.

## Homework

### Part 1

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).  
   Создан репозиторий `TiMP` на сервисе github.com.

2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдущем шаге.

```bash
vboxuser@FirstTiMP:~/TiMP$ echo "# Hello World C++" > README.md
vboxuser@FirstTiMP:~/TiMP$ git add README.md
vboxuser@FirstTiMP:~/TiMP$ git commit -m "Initial commit"
```

Вывод:

```
[main (root-commit) 7886151] Initial commit
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

```bash
vboxuser@FirstTiMP:~/TiMP$ git push -u origin main
```

Вывод:

```
Username for 'https://github.com': wat2344
Password for 'https://wat2344@github.com':
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 237 bytes | 237.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/wat2344/TiMP.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу Hello world на языке C++, используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.

```bash
vboxuser@FirstTiMP:~/TiMP$ cat > hello_world.cpp << 'EOF'
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
EOF
```

Выполнено, файл с кодом создан.

4. Добавьте этот файл в локальную копию репозитория.

```bash
vboxuser@FirstTiMP:~/TiMP$ git add hello_world.cpp
```

5. Закоммитьте изменения с осмысленным сообщением.

```bash
vboxuser@FirstTiMP:~/TiMP$ git commit -m "Add hello_world.cpp"
```

Вывод:

```
[main 2f94d26] Add hello_world.cpp
 1 file changed, 7 insertions(+)
 create mode 100644 hello_world.cpp
```

6. Измените исходный код так, чтобы программа через стандартный поток ввода запрашивала имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` — имя пользователя.

```bash
vboxuser@FirstTiMP:~/TiMP$ nano hello_world.cpp
```

Заменено содержимое файла на:

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string name;
    cout << "Enter your name: ";
    getline(cin, name);
    cout << "Hello world from " << name << endl;
    return 0;
}
```

7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?

```bash
vboxuser@FirstTiMP:~/TiMP$ git commit -am "Add user input"
```

Вывод:

```
[main 3c1866b] Add user input
 1 file changed, 5 insertions(+), 1 deletion(-)
```

После первого коммита файл `hello_world.cpp` уже отслеживается Git-ом, поэтому `git add` писать больше не нужно.

8. Запушьте изменения в удалённый репозиторий.

```bash
vboxuser@FirstTiMP:~/TiMP$ git push
```

Вывод:

```
Username for 'https://github.com': wat2344
Password for 'https://wat2344@github.com':
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 6 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 791 bytes | 791.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/wat2344/TiMP.git
   7886151..3c1866b  main -> main
```

9. Проверьте, что история коммитов доступна в удалённом репозитории.

```bash
vboxuser@FirstTiMP:~/TiMP$ git log
```

Вывод:

```
commit 3c1866b64460cd240e096bfbcb147b1bf2d38138 (HEAD -> main, origin/main)
Author: wat2344 <pavel.khokhlov.07@inbox.ru>
Date:   Sat Apr 25 15:20:36 2026 +0000

    Add user input

commit 2f94d2624a2054b8e98eb38dfe4b7de1c0aa4ef9
Author: wat2344 <pavel.khokhlov.07@inbox.ru>
Date:   Sat Apr 25 15:16:04 2026 +0000

    Add hello_world.cpp

commit 7886151e3ad518cdbcd9bbd9784e1693a6a70691
Author: wat2344 <pavel.khokhlov.07@inbox.ru>
Date:   Sat Apr 25 15:05:18 2026 +0000

    Initial commit
```

### Part 2

1. В локальной копии репозитория создайте локальную ветку `patch1`.

```bash
vboxuser@FirstTiMP:~/TiMP$ git checkout -b patch1
```

Вывод:

```
Switched to a new branch 'patch1'
```

2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.

```bash
vboxuser@FirstTiMP:~/TiMP$ nano hello_world.cpp
```

Заменён код на:

```cpp
#include <iostream>
#include <string>

int main() {
    std::string name;
    std::cout << "Enter your name: ";
    std::getline(std::cin, name);
    std::cout << "Hello world from " << name << std::endl;
    return 0;
}
```

3. Commit, push локальную ветку в удалённый репозиторий.

```bash
vboxuser@FirstTiMP:~/TiMP$ git commit -am "Remove using namespace std"
```

Вывод:

```
[patch1 60abf93] Remove using namespace std
 1 file changed, 4 insertions(+), 5 deletions(-)
```

```bash
vboxuser@FirstTiMP:~/TiMP$ git push -u origin patch1
```

Вывод:

```
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 6 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 439 bytes | 439.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
remote: 
remote: Create a pull request for 'patch1' on GitHub by visiting:
remote:      https://github.com/wat2344/TiMP/pull/new/patch1
remote: 
To https://github.com/wat2344/TiMP.git
 * [new branch]      patch1 -> patch1
branch 'patch1' set up to track 'origin/patch1'.
```

4. Проверьте, что ветка `patch1` доступна в удалённом репозитории.  
   Ветку на GitHub вижу.

5. Создайте pull-request `patch1 -> master`.  
   Нажал «Compare & pull request» на GitHub.

6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.

```bash
vboxuser@FirstTiMP:~/TiMP$ nano hello_world.cpp
```

Добавлены комментарии в код:

```cpp
#include <iostream>
#include <string>

int main() {
    // Запрашиваем имя пользователя
    std::string name;
    std::cout << "Enter your name: ";
    std::getline(std::cin, name);

    // Выводим приветствие
    std::cout << "Hello world from " << name << std::endl;
    return 0;
}
```

7. Commit, push.

```bash
vboxuser@FirstTiMP:~/TiMP$ git commit -am "Add comments"
```

Вывод:

```
[patch1 d605d88] Add comments
 1 file changed, 3 insertions(+)
```

```bash
vboxuser@FirstTiMP:~/TiMP$ git push
```

Вывод:

```
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 6 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 409 bytes | 409.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/wat2344/TiMP.git
   60abf93..d605d88  patch1 -> patch1
```

8. Проверьте, что новые изменения есть в созданном на шаге 5 pull-request.  
   На GitHub изменения видны.

9. В удалённом репозитории выполните слияние PR `patch1 -> master` и удалите ветку `patch1` в удалённом репозитории.  
   Слияние выполнено.

10. Локально выполните pull.

```bash
vboxuser@FirstTiMP:~/TiMP$ git checkout main
```

Вывод:

```
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
```

```bash
vboxuser@FirstTiMP:~/TiMP$ git pull
```

Вывод:

```
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (1/1), 898 bytes | 898.00 KiB/s, done.
From https://github.com/wat2344/TiMP
   3c1866b..8e77a11  main       -> origin/main
Updating 3c1866b..8e77a11
Fast-forward
 hello_world.cpp | 12 +++++++-----
 1 file changed, 7 insertions(+), 5 deletions(-)
```

11. С помощью команды `git log` просмотрите историю в локальной версии ветки `master`.

```bash
vboxuser@FirstTiMP:~/TiMP$ git log --oneline --graph
```

Вывод:

```
*   8e77a11 (HEAD -> main, origin/main, origin/HEAD) Merge pull request #1 from wat2344/patch1
|\  
| * d605d88 (origin/patch1, patch1) Add comments
| * 60abf93 Remove using namespace std
|/  
* 3c1866b Add user input
* 2f94d26 Add hello_world.cpp
* 7886151 Initial commit
```

12. Удалите локальную ветку `patch1`.

```bash
vboxuser@FirstTiMP:~/TiMP$ git branch -d patch1
```

Вывод:

```
Deleted branch patch1 (was d605d88).
```

### Part 3

1. Создайте новую локальную ветку `patch2`.

```bash
vboxuser@FirstTiMP:~/TiMP$ git checkout -b patch2
```

Вывод:

```
Switched to a new branch 'patch2'
```

2. Измените code style с помощью утилиты `clang-format`. Например, используя опцию `-style=Mozilla`.

```bash
vboxuser@FirstTiMP:~/TiMP$ clang-format -i -style=Mozilla hello_world.cpp
```

Вывода не последовало, но содержимое файла теперь выглядит так:

```cpp
#include <iostream>
#include <string>

int
main()
{
  // Запрашиваем имя пользователя
  std::string name;
  std::cout << "Enter your name: ";
  std::getline(std::cin, name);

  // Выводим приветствие
  std::cout << "Hello world from " << name << std::endl;
  return 0;
}
```

3. Commit, push, создайте pull-request `patch2 -> master`.

```bash
vboxuser@FirstTiMP:~/TiMP$ git commit -am "Apply Mozilla code style"
```

Вывод:

```
[patch2 626a5f8] Apply Mozilla code style
 1 file changed, 10 insertions(+), 8 deletions(-)
```

```bash
vboxuser@FirstTiMP:~/TiMP$ git push -u origin patch2
```

Вывод:

```
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 6 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 386 bytes | 386.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote: 
remote: Create a pull request for 'patch2' on GitHub by visiting:
remote:      https://github.com/wat2344/TiMP/pull/new/patch2
remote: 
To https://github.com/wat2344/TiMP.git
 * [new branch]      patch2 -> patch2
branch 'patch2' set up to track 'origin/patch2'.
```

Pull request создан на GitHub.

4. В ветке `master` в удалённом репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.  
   В GitHub изменил содержимое `hello_world.cpp` на:

```cpp
#include <iostream>
#include <string>

int main() {
    // Requesting person's name
    std::string name;
    std::cout << "Enter your name: ";
    std::getline(std::cin, name);

    // Sending greetings
    std::cout << "Hello world from " << name << std::endl;
    return 0;
}
```

5. Убедитесь, что в pull-request появились конфликты.  
   Конфликт показывает.

6. Для этого локально выполните `pull + rebase` (точную последовательность команд следует узнать самостоятельно). Исправьте конфликты.

```bash
vboxuser@FirstTiMP:~/TiMP$ git fetch origin
```

Вывод:

```
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 1.03 KiB | 1.03 MiB/s, done.
From https://github.com/wat2344/TiMP
   8e77a11..e795655  main       -> origin/main
```

```bash
vboxuser@FirstTiMP:~/TiMP$ git rebase origin/main
```

Вывод:

```
Auto-merging hello_world.cpp
CONFLICT (content): Merge conflict in hello_world.cpp
error: could not apply 626a5f8... Apply Mozilla code style
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
hint: Disable this message with "git config set advice.mergeConflict false"
Could not apply 626a5f8... # Apply Mozilla code style
```

Внутри файла `hello_world.cpp` удаляю вторую версию (из patch 2). Теперь он выглядит так:

```cpp
#include <iostream>
#include <string>

int main() {
    // Requesting person's name
    std::string name;
    std::cout << "Enter your name: ";
    std::getline(std::cin, name);

    // Sending greetings
    std::cout << "Hello world from " << name << std::endl;
    return 0;
}
```

```bash
vboxuser@FirstTiMP:~/TiMP$ git add hello_world.cpp
vboxuser@FirstTiMP:~/TiMP$ git rebase --continue
```

Вывод:

```
Successfully rebased and updated refs/heads/patch2.
```

7. Сделайте force push в ветку `patch2`.

```bash
vboxuser@FirstTiMP:~/TiMP$ git push --force-with-lease origin patch2
```

Вывод:

```
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/wat2344/TiMP.git
 + 626a5f8...e795655 patch2 -> patch2 (forced update)
```

8. Убедитесь, что в pull-request пропали конфликты.  
   Ветки оказались одинаковыми, пришлось добавить дополнительный комментарий. В целом моя ошибка, нужно было оставить с изменённым стилем кода, тогда было бы нормально, но никто не говорил оставить именно вторую версию, и задача в итоге выполнена, так что проблем не вижу.

```bash
vboxuser@FirstTiMP:~/TiMP$ echo "// extra comment" >> hello_world.cpp
vboxuser@FirstTiMP:~/TiMP$ git commit -am "Add dummy comment to enable PR"
```

Вывод:

```
[patch2 989b60f] Add dummy comment to enable PR
 1 file changed, 1 insertion(+)
```

```bash
vboxuser@FirstTiMP:~/TiMP$ git push origin patch2
```

Вывод:

```
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 6 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 349 bytes | 349.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/wat2344/TiMP.git
   e795655..989b60f  patch2 -> patch2
```

Теперь конфликтов нет и merge стал доступен.

9. Вмержите pull-request `patch2 -> master`.  
```
Merge выполнен.
```
