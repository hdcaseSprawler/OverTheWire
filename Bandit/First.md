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

  SSH: ssh bandit11@bandit.labs.overthewire.org -p 2220
  Password: dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
Пароль для следующего уровня хранится в файле data.txt, где все строчные (az) и прописные (AZ) буквы повернуты на 13 позиций

Я использовал онлайн шифр цезаря и сдвинул символы на 13:
> cat data.txt 
Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4


  ## Level 12 -> 13 - Walkthrough

  SSH: ssh bandit12@bandit.labs.overthewire.org -p 2220
  Password: 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
Пароль находится в многократно пересжатом файле data.txt и нам необходимо размотать цепочку и выйти на финальный файл:

Создаем рабочую директорию в которой будем производить все манипуляции и копируем туда исходный файл
> mkdir /tmp/bandit_decomp
> file data.txt 
data.txt: ASCII text
> xxd -r data.txt > binary_data.bin -- преобразуем шестнадцатеричное представление данных обратно в двоичные данные
> file binary_data.bin 
binary_data.bin: gzip compressed data, was "data2.bin", last modified: Thu Sep 19 07:08:15 2024, max compression, from Unix, original size modulo 2^32 574
> file binary_data.bin 
binary_data.bin: gzip compressed data, was "data2.bin", last modified: Thu Sep 19 07:08:15 2024, max compression, from Unix, original size modulo 2^32 574
> mv binary_data.bin binary_data.gz -- переименовываем файл в нужный формат
> gunzip binary_data.gz
> file binary_data 
binary_data: bzip2 compressed data, block size = 900k
> bunzip2 binary_data
bunzip2: Can't guess original name for binary_data -- using binary_data.out
> file binary_data.out 
binary_data.out: gzip compressed data, was "data4.bin", last modified: Thu Sep 19 07:08:15 2024, max compression, from Unix, original size modulo 2^32 20480
> mv binary_data.out binary_data.gz
> gunzip binary_data.gz
> file binary_data 
binary_data: POSIX tar archive (GNU)
> mv binary_data binary_data.tar
> tar xfv binary_data.tar
data5.bin
> file data5.bin 
data5.bin: POSIX tar archive (GNU)
> mv data5.bin data5.tar
> tar xfv data5.tar 
data6.bin
> file data6.bin 
data6.bin: bzip2 compressed data, block size = 900k
> mv data6.bin data6
> bunzip2 data6
bunzip2: Can't guess original name for data6 -- using data6.out
> file data6.out 
data6.out: POSIX tar archive (GNU)
> mv data6.out data6.tar
> tar xfv data6.tar 
data8.bin
> file data8.bin 
data8.bin: gzip compressed data, was "data9.bin", last modified: Thu Sep 19 07:08:15 2024, max compression, from Unix, original size modulo 2^32 49
> mv data8.bin data8.gz
> gunzip data8.gz
> file data8 
data8: ASCII text
> cat data8 
The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn

  ## Level 13 -> 14 - Walkthrough

  SSH: ssh bandit13@bandit.labs.overthewire.org -p 2220
  Password: FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
Пароль для следующего уровня хранится в файле /etc/bandit_pass/bandit14 и может быть прочитан только пользователемbandit14. На этом уровне вы не получаете следующий пароль, но получаете закрытый ключ SSH, который можно использовать для входа на следующий уровень. Примечание. localhost — это имя хоста, которое относится к машине, на которой вы работаете

Убеждаемся в существовании ключа:
> ls
sshkey.private
> exit

Получаем sshkey.private с удаленного сервера на свою машину:
> scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private . -- scp позволяет копировать файл по защищенному соединению.
Вводим пароль от уровня

Далее со своей машины заходим на 14 уровень:
> ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
и получаем предупреждение о доступе к файлу sshkey.private
> chmod 700 sshkey.private

И заходим на 14 уровень:
> ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220

  ## Level 14 -> 15 - Walkthrough

  SSH: ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
  Password: -
Пароль для следующего уровня можно получить, отправив пароль текущего уровня на порт 30000 на localhost
Соответственно, необходимо найти пароль в /etc/bandit_pass/bandit
> cat /etc/bandit_pass/bandit14 
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
> nc localhost 30000 -- устанавливаем содинение на указанном порту и передаем пароль
> Correct!
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

  ## Level 15 -> 16 - Walkthrough

  SSH: ssh bandit15@bandit.labs.overthewire.org -p 2220
  Password: 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
Пароль для следующего уровня можно получить, отправив пароль текущего уровня на порт 30001 на локальном хосте с использованием шифрования SSL/TLS.
Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.

> cat /etc/bandit_pass/bandit15
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
> openssl s_client -connect localhost:30001 -- используется для создания SSL/TLS соединения с localhost:30001 
Correct!
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
closed

  ## Level 16 -> 17 - Walkthrough

  SSH: ssh bandit16@bandit.labs.overthewire.org -p 2220
  Password: kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
Учетные данные для следующего уровня можно получить, отправив пароль текущего уровня на порт на локальном хосте в диапазоне от 31000 до 32000. Сначала выясните, какие из этих портов прослушивает сервер. Затем выясните, какие из них поддерживают SSL/TLS, а какие нет. Есть только один сервер, который предоставит следующие учетные данные, остальные просто отправят вам обратно все, что вы на него отправите.

> cat /etc/bandit_pass/bandit16
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
Далее два варианта
  Первый (Быстрый)
> nc -zv localhost 31000-32000 -- с помощью netcat сканируем диапазон портов
Connection to localhost (127.0.0.1) 31046 port [tcp/*] succeeded!
Connection to localhost (127.0.0.1) 31518 port [tcp/*] succeeded!
Connection to localhost (127.0.0.1) 31691 port [tcp/*] succeeded!
Connection to localhost (127.0.0.1) 31790 port [tcp/*] succeeded!
Connection to localhost (127.0.0.1) 31960 port [tcp/*] succeeded!
> далее нужно подобрать порт и подключиться

  Второй (удобный)
> nmap -sV localhost -p 31000-32000
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00018s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo -- echo сервер
31691/tcp open  echo
31790/tcp open  ssl/unknown -- многообещающий
31960/tcp open  echo

Я очень долго не мог получить RSA ключ, потому что при использовании openssl s_client -ign_eof -connect localhost:31790 и вводе пароля я получал вывод KEYUPDATE и все, потом на StackOwerflow я увидел возможное решение проблемы:
echo 'kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx' | openssl s_client -ign_eof -connect localhost:31790
и получил ключ. Скопировал его, вышел в свою машину, и скопировав файл из уровня 14 заменил в нем ключ и сохранил под именем sshkey.private17
Следующий уровень

  ## Level 17 -> 18 - Walkthrough

  SSH: ssh -i sshkey.private17 bandit17@bandit.labs.overthewire.org -p 2220
  Password: -
В домашнем каталоге есть 2 файла: passwords.old и passwords.new. Пароль для следующего уровня находится в файле passwords.new и является единственной строкой, которая была изменена между passwords.old и passwords.new

> diff passwords.old passwords.new 
42c42
< ktfgBvpMzWKR5ENj26IbLGSblgUG9CzB
---
> x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO


  ## Level 18 -> 19 - Walkthrough

  SSH: ssh bandit18@bandit.labs.overthewire.org -p 2220
  Password: x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
Пароль для следующего уровня хранится в файле readme в домашнем каталоге. К сожалению, кто-то изменил .bashrc, чтобы при входе в систему по SSH меня сразу выкидывало с ВМ

Решение:
> echo "cat readme" | ssh bandit18@bandit.labs.overthewire.org -p 2220
> вводим пароль и меня сразу выкидывает, но уже с выводом readme:
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8

  ## Level 19 -> 20 - Walkthrough

  SSH: ssh bandit19@bandit.labs.overthewire.org -p 2220
  Password: cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
Чтобы получить доступ к следующему уровню, следует использовать двоичный файл setuid в домашнем каталоге. Выполните его без аргументов, чтобы узнать, как его использовать. Пароль для этого уровня можно найти в обычном месте (/etc/bandit_pass), после того как вы использовали бинарный файл setuid

Разрешения Linux — очень большая тема. У каждого файла есть владелец и группа, которой принадлежит файл. Для пользователя, группы и остальных пользователей разрешения могут быть установлены отдельно. Его можно выбрать, если файл доступен для чтения, записи или исполнения. Разрешения и владельцев файла можно увидеть с помощью команды ls -l. В третьем столбце отображается пользователь, в четвертом — группа, а в первом столбце — разрешения. Разрешения записываются следующим образом: rwxrwxrwx, первые три буквы указывают, что у пользователя есть все разрешения (чтение=r, запись=w и выполнение=x). Следующие три буквы обозначают разрешение группы и последняя — всех остальных. Если одна из букв заменена на -, это означает, что разрешение не предоставлено.
Suid – это специальное разрешение. Он заменит x в разрешении пользователя. Это означает, что двоичный файл будет запускаться от имени владельца двоичного файла, а не от имени того, кто его выполняет. Чтобы предоставить двоичным разрешениям suid, необходимо использовать следующую команду: chmod u+s <имя файла>.

> ls -l
total 16
-rwsr-x--- 1 bandit20 bandit19 14880 Sep 19 07:08 bandit20-do
> 
В данном случае владельцем является badit20, а группой являетсяbandit19. Это с '-rwsr-x—' означает, что пользователь bandit19 может выполнять двоичный файл, но двоичный файл выполняется от имени пользователяbandit20.
Выполнение двоичного файла говорит о том, что он просто выполняет другую команду от имени другого пользователя (как уже объяснялось, этот пользователь —bandit20). Это означает, что мы можем получить доступ к файлу паролей пользователей bandit20, который может прочитать только пользователь bandit20.

> ./bandit20-do 
Run a command as another user.
  Example: ./bandit20-do id
> ./bandit20-do id
uid=11019(bandit19) gid=11019(bandit19) euid=11020(bandit20) groups=11019(bandit19)
> cat /etc/bandit_pass/bandit20 
cat: /etc/bandit_pass/bandit20: Permission denied
> ./bandit20-do cat /etc/bandit_pass/bandit20
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO

Т.е. скрипт bandit20-do позволяет нам получить доступ к файлам, относящимся к пользователю bandit20 -- [howTo](https://github.com/hdcaseSprawler/setuid/tree/main)


  ## Level 20 -> 21 - Walkthrough

  SSH: ssh bandit20@bandit.labs.overthewire.org -p 2220
  Password: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
В домашнем каталоге находится двоичный файл setuid, который выполняет следующие действия: устанавливает соединение с localhost через порт, указанный вами в качестве аргумента командной строки. Затем он считывает строку текста из соединения и сравнивает ее с паролем на предыдущем уровне (bandit20). Если пароль правильный, он передаст пароль для следующего уровня (bandit21).

ПРИМЕЧАНИЕ. Попробуйте подключиться к своему сетевому демону и проверить, работает ли он так, как вы думаете

В домашнем каталоге находится двоичный файл setuid, который выполняет следующие действия: устанавливает соединение с localhost через порт, указанный вами в качестве аргумента командной строки. Затем он считывает строку текста из соединения и сравнивает ее с паролем на предыдущем уровне (bandit20). Если пароль правильный, он передаст пароль для следующего уровня (bandit21).
ПРИМЕЧАНИЕ. Попробуйте подключиться к своему сетевому демону и проверить, работает ли он так, как вы думаете

Используя «netcat», мы можем создать соединение в режиме сервера, которое прослушивает входящие соединения. Чтобы Netcat отправил пароль, я использую echo и передаю его в netcat. Флаг -n предназначен для предотвращения ввода символов новой строки. Наконец, мы позволяем процессу работать в фоновом режиме с помощью &:
> echo -n '0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO' | nc -l -p 1234 &

Запуск двоичного файла setuid с портом 1234 означает, что он подключится к нашему серверу netcat, получит пароль, введенный через echo, и отправит обратно следующий пароль:
> ./suconnect 1234
Read: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
Password matches, sending next password
EeoULMCra2q0dSkYj561DX7s1CpBuOBt

  ## Level 20 -> 21 - Walkthrough

  SSH: ssh bandit21@bandit.labs.overthewire.org -p 2220
  Password: EeoULMCra2q0dSkYj561DX7s1CpBuOBt
Программа запускается автоматически через регулярные промежутки времени из cron, планировщика заданий, основанного на времени. Посмотрите в /etc/cron.d/ конфигурацию и посмотрите, какая команда выполняется

