Bandit

The Bandit wargame is aimed at absolute beginners. It will teach the basics needed to be able to play other wargames.

  ## Level 0 -> 1 - Walkthrough

  SSH: ssh bandit0@bandit.labs.overthewire.org -p 2220
  Password: bandit0
Необходимо подключиться по SSH к удаленному серверу и прочитать readme файл с паролем к следующему уровню:
  > ls
  readme
  > cat readme
  ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
С помощью этого пароля переходим на следующий уровень

  ## Level 1 -> 2 - Walkthrough

  SSH: ssh bandit1@bandit.labs.overthewire.org -p 2220
  Password: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
Необходимо получить пароль из файла с названием '-'
Так как в терминале при вводе команды символ '-' воспринимается как флаг, для корректного отображения необходимо указать абсолютный путь к файлу:
  > cat ./-
  263JGJPfgU6LtdEvgfWU1XP5yac29mFx
Переходим на следующий уровень

  ## Level 2 -> 3 - Walkthrough

  SSH: ssh bandit2@bandit.labs.overthewire.org -p 2220
  Password: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx
Пароль находится в файле 'spaces in this filename', в названии файла содержатся пробелы, есть несколько вариантов решения
-Экранирование:
  > cat spaces\ in\ this\ filename
-Кавычки:
  > cat "spaces in this filename"
-Tab:
  bandit2@bandit:~$ cat 'spaces' и нажать tab
  MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
Следующий уровень

  ## Level 3 -> 4 - Walkthrough

  SSH: ssh bandit3@bandit.labs.overthewire.org -p 2220
  Password: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

Пароль находится в скрытом файле в папке inhere, получаем с помощью cat и отображением скрытых файлов через ls -a:
  > cd inhere/
  > ls -a
  > cat .hidden
  2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
Далее

  ## Level 4 -> 5 - Walkthrough

  SSH: ssh bandit4@bandit.labs.overthewire.org -p 2220
  Password: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
Пароль для следующего уровня хранится в единственном удобочитаемом файле во внутренней директории. Совет: если у вас сломался терминал, попробуйте команду «reset».

Я использовал команду file для отображения формата, для рекурсивной обработки содержимого директории:
find ./inhere/ -type f -exec file {} +
где:
- find ./inhere/ - начинает поиск в директории ./inhere/
- -type f - указывает, что мы ищем только файлы
- -exec file {} + - для каждого найденного файла запускает команду file

> find ./inhere/ -type f -exec file {} +
./inhere/-file05: data
./inhere/-file07: ASCII text
./inhere/-file03: data
> cat inhere/-file07
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

  ## Level 5 -> 6 - Walkthrough

  SSH: ssh bandit5@bandit.labs.overthewire.org -p 2220
  Password: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
Пароль находится в файле, отвечающем требованиям:
- human-readable
- 1033 bytes in size
- not executable

Дополнил предыдущую команду чтобы отфильтровать и найти только нужный файл:
> find ./inhere/ -type f -size 1033c ! -executable -exec file {} +
> ./inhere/maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

  ## Level 6 -> 7 - Walkthrough

  SSH: SSH: ssh bandit6@bandit.labs.overthewire.org -p 2220
  Password: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
Пароль находится где то на сервере и отвечает требованиям:
- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

При вводе ls и ls -a выводится:
.  ..  .bash_logout  .bashrc  .profile

Использовал команду:
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
где:
- find / начать поиск от корневой директории
- -type f искать только файлы
- -user bandit7 файлы, принадлежащие пользователю bandit7
- -group bandit6 файлы, принадлежащие группе bandit6
- -size 33c файлы размером 33 байта
- 2>/dev/null подавить ошибки доступа

> find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
> cat /var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

  ## Level 7 -> 8 - Walkthrough

  SSH: ssh bandit7@bandit.labs.overthewire.org -p 2220
  Password: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
Пароль для следующего уровня хранится в файле data.txt после словф millionth

Использовал команду:
grep -A1 "millionth" /path/to/data.txt | head -n1
где:
- -A1 означает "append one line after match".
- head -n1 ограничивает вывод одной строкой

> grep -A1 "millionth" /path/to/data.txt | head -n1
millionth	dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

  ## Level 8 -> 9 - Walkthrough

  SSH: ssh bandit8@bandit.labs.overthewire.org -p 2220
  Password: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
Пароль для следующего уровня хранится в файле data.txt и представляет собой единственную строку текста, которая встречается только один раз

Использовал команду для сортировки и вывода уникальных значений:

> sort data.txt | uniq -u
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM


  ## Level 9 -> 10 - Walkthrough

  SSH: ssh bandit9@bandit.labs.overthewire.org -p 2220
  Password: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
Пароль для следующего уровня хранится в файле data.txt в виде одной из немногих удобочитаемых строк, которым предшествует несколько символов «=».
Тут все просто, cat data.txt и нашел вручную пароль, так как не разобрался с командами из за возможности множественных знаков "="

FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

  ## Level 10 -> 11 - Walkthrough

  SSH: ssh bandit10@bandit.labs.overthewire.org -p 2220
  Password: FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
Пароль для следующего уровня хранится в файле data.txt, который содержит данные в кодировке Base64

Использовал базовую утилиту base64 для декодирования файла:
> cat data.txt
> VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
> base64 -d data.txt
> The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

  ## Level 11 -> 12 - Walkthrough

  SSH: ssh bandit10@bandit.labs.overthewire.org -p 2220
  Password: dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
Пароль
