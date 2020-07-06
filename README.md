## Урок 8

### 1. Вывести на экран 3 раза имя пользователя, от которого запускается команда.

```sh
ubuntu@ip-172-31-45-100:~$ for i in {seq 1 3}; do users; done
ubuntu
ubuntu
ubuntu
```

### 2. Вывести с помощью цикла while все четные числа от 0 до 100 включительно.

```sh
ubuntu@ip-172-31-45-100:~$ i=0; while [ $i -le 100 ]; do if [ $(($i % 2)) -eq 0 ]; then echo $i; fi; i=$(($i+1)); done
0
2
4
6
8
10
12
14
16
18
20
22
24
26
28
30
32
34
36
38
40
42
44
46
48
50
52
54
56
58
60
62
64
66
68
70
72
74
76
78
80
82
84
86
88
90
92
94
96
98
100
```

### 3. Создать с помощью nano файл test.txt. Настроить автоматический бэкап этого файла раз в 10 минут в файл с названием test.txt.bak с использованием cron.


Создаем файл

```sh
ubuntu@ip-172-31-45-100:~$ nano test.txt
ubuntu@ip-172-31-45-100:~$ cat test.txt
test
```

Создаем задачу в cron

```sh
ubuntu@ip-172-31-45-100:~$ crontab -e
no crontab for ubuntu - using an empty one

Select an editor.  To change later, run 'select-editor'.
  1. /bin/nano        <---- easiest
  2. /usr/bin/vim.basic
  3. /usr/bin/vim.tiny
  4. /bin/ed

Choose 1-4 [1]: 2
crontab: installing new crontab
ubuntu@ip-172-31-45-100:~$ crontab -l
# Edit this file to introduce tasks to be run by cron.
# 
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
# 
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').
# 
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
# 
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
# 
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
# 
# For more information see the manual pages of crontab(5) and cron(8)
# 
# m h  dom mon dow   command

*/10 * * * *	/home/ubuntu/backup.sh
```

Создаем скрипт для резервного копирования

```sh
ubuntu@ip-172-31-45-100:~$ vi backup.sh
ubuntu@ip-172-31-45-100:~$ chmod +x backup.sh
ubuntu@ip-172-31-45-100:~$ cat backup.sh
#!/bin/bash

if [ -f /home/ubuntu/test.txt ]
then
	cp /home/ubuntu/test.txt /home/ubuntu/test.txt.bak
fi
```

Записи журнала работы cron

```sh
ubuntu@ip-172-31-45-100:~$ sudo tail -f /var/log/syslog | grep -i cron
Jul  6 21:01:56 ip-172-31-45-100 crontab[4937]: (ubuntu) BEGIN EDIT (ubuntu)
Jul  6 21:03:02 ip-172-31-45-100 crontab[4937]: (ubuntu) REPLACE (ubuntu)
Jul  6 21:03:02 ip-172-31-45-100 crontab[4937]: (ubuntu) END EDIT (ubuntu)
Jul  6 21:03:39 ip-172-31-45-100 crontab[4963]: (ubuntu) LIST (ubuntu)
Jul  6 21:04:23 ip-172-31-45-100 crontab[4964]: (ubuntu) BEGIN EDIT (ubuntu)
Jul  6 21:04:44 ip-172-31-45-100 crontab[4964]: (ubuntu) REPLACE (ubuntu)
Jul  6 21:04:44 ip-172-31-45-100 crontab[4964]: (ubuntu) END EDIT (ubuntu)
Jul  6 21:05:01 ip-172-31-45-100 cron[493]: (ubuntu) RELOAD (crontabs/ubuntu)
Jul  6 21:10:01 ip-172-31-45-100 CRON[4987]: (ubuntu) CMD (/home/ubuntu/backup.sh)
Jul  6 21:17:01 ip-172-31-45-100 CRON[5016]: (root) CMD (   cd / && run-parts --report /etc/cron.hourly)
Jul  6 21:20:01 ip-172-31-45-100 CRON[5020]: (ubuntu) CMD (/home/ubuntu/backup.sh)
```

Резервная копия

```sh
ubuntu@ip-172-31-45-100:~$ ls test.txt* -l
-rw-rw-r-- 1 ubuntu ubuntu 5 Jul  6 21:01 test.txt
-rw-rw-r-- 1 ubuntu ubuntu 5 Jul  6 21:20 test.txt.bak
ubuntu@ip-172-31-45-100:~$ cat test.txt.bak 
test
```
