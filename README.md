## Урок 4

### 1. Создать пользователя user_new и предоставить ему права на редактирование файла с программой, выводящей на экран Hello, world!

```sh
ubuntu@ip-172-31-45-100:~$ sudo useradd -m -s /bin/bash user_new
ubuntu@ip-172-31-45-100:~$ sudo passwd user_new
New password: 
Retype new password: 
passwd: password updated successfully
ubuntu@ip-172-31-45-100:~$ id user_new
uid=1001(user_new) gid=1001(user_new) groups=1001(user_new)
ubuntu@ip-172-31-45-100:~$ cat /etc/passwd | grep 'user_new'
user_new:x:1001:1001::/home/user_new:/bin/bash
ubuntu@ip-172-31-45-100:~$ sudo groupadd editors
ubuntu@ip-172-31-45-100:~$ sudo usermod -G editors ubuntu
ubuntu@ip-172-31-45-100:~$ sudo usermod -G editors user_new
ubuntu@ip-172-31-45-100:~$ sudo chown ubuntu:editors hello.py 
ubuntu@ip-172-31-45-100:~$ ls -l hello.py 
-rw-rw-r-- 1 ubuntu editors 23 Jun 21 16:07 hello.py
```

### 2. Зайти под юзером user_new и с помощью редактора Vim поменять фразу в скрипте из пункта 1 на любую другую.

```sh
ubuntu@ip-172-31-45-100:~$ su user_new
Password: 
user_new@ip-172-31-45-100:/home/ubuntu$ ls -l hello.py 
-rw-rw-r-- 1 ubuntu editors 23 Jun 21 16:07 hello.py
user_new@ip-172-31-45-100:/home/ubuntu$ vi hello.py 
user_new@ip-172-31-45-100:/home/ubuntu$ cat hello.py 
print("Hi there!")
user_new@ip-172-31-45-100:/home/ubuntu$ python3 hello.py 
Hi there!
```

### 3.\* Под юзером user_new зайти в его домашнюю директорию и создать программу на Python, выводящую в консоль цифры от 1 до 10 включительно с интервалом в 1 секунду.

```sh
user_new@ip-172-31-45-100:/home/ubuntu$ cd
user_new@ip-172-31-45-100:~$ pwd
/home/user_new
user_new@ip-172-31-45-100:~$ vi count10.py
user_new@ip-172-31-45-100:~$ cat count10.py 
from time import sleep

for i in range(10):
    print(i+1)
    sleep(1)
user_new@ip-172-31-45-100:~$ python3 count10.py
1
2
3
4
5
6
7
8
9
10
```
