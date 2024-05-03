Bandit

The Bandit wargame is aimed at absolute beginners. It will teach the basics needed to be able to play other wargames.

  Level 0 -> 1 - Walkthrough

  SSH: ssh bandit0@bandit.labs.overthewire.org -p 2220
  Password: bandit0
Необходимо подключиться по SSH к удаленному серверу и прочитать readme файл с паролем к следующему уровню:
  bandit0@bandit:~$ ls
  readme
  bandit0@bandit:~$ cat readme
  boJ9jbbUNNfktd78OOpsqOltutMc3MY1
С помощью этого пароля переходим на следующий уровень

  Level 1 -> 2 - Walkthrough

  SSH: ssh bandit1@bandit.labs.overthewire.org -p 2220
  Password: boJ9jbbUNNfktd78OOpsqOltutMc3MY1
Необходимо получить пароль из файла с названием '-'
Так как в терминале при вводе команды символ '-' воспринимается как флаг, для корректного отображения необходимо указать абсолютный путь к файлу:
  bandit1@bandit:~$ cat ./-
  rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
Переходим на следующий уровень

  Level 2 -> 3 - Walkthrough

  SSH: ssh bandit2@bandit.labs.overthewire.org -p 2220
  Password: rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
Пароль находится в файле 'spaces in this filename', в названии файла содержатся пробелы, есть несколько вариантов решения
-Экранирование:
  bandit2@bandit:~$ cat spaces\ in\ this\ filename
-Кавычки:
  bandit2@bandit:~$ cat "spaces in this filename"
-Tab:
  bandit2@bandit:~$ cat 'spaces' и нажать tab
  aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
Следующий уровень

  Level 3 -> 4 - Walkthrough

  SSH: ssh bandit3@bandit.labs.overthewire.org -p 2220
  Password: aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG

Пароль находится в скрытом файле в папке inhere, получаем с помощью cat и отображением скрытых файлов через ls -a:
  bandit3@bandit:~$ cd inhere/
  bandit3@bandit:~/inhere$ ls -a
  bandit3@bandit:~/inhere$ cat .hidden
  2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
Далее

Level 3 -> 4 - Walkthrough

  SSH: ssh bandit3@bandit.labs.overthewire.org -p 2220
  Password: 2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
Пароль для следующего уровня хранится в единственном удобочитаемом файле во внутренней директории. Совет: если у вас сломался терминал, попробуйте команду «reset».

  bandit4@bandit:~$ cat inhere/-file07
  lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR

Level 4 -> 5 - Walkthrough

  SSH: SSH: ssh bandit4@bandit.labs.overthewire.org -p 2220
  Password: lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR


