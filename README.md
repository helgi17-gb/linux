## Урок 2

### 1. Создать каталоги first и second в домашней директории, а в них — текстовые файлы first.py и second.py, содержащие программы, выводящие на экран числа 1 и 2 соответственно. 

```sh
ubuntu@ip-172-31-16-144:~$ cd
ubuntu@ip-172-31-16-144:~$ mkdir first second
ubuntu@ip-172-31-16-144:~$ ls
first  second
ubuntu@ip-172-31-16-144:~$ echo "print('1')" > first/first.py
ubuntu@ip-172-31-16-144:~$ ls first
first.py
ubuntu@ip-172-31-16-144:~$ cat first/first.py
print('1')
ubuntu@ip-172-31-16-144:~$ echo "print('2')" > second/second.py
ubuntu@ip-172-31-16-144:~$ ls second
second.py
ubuntu@ip-172-31-16-144:~$ cat second/second.py
print('2')
```

### 2. Переместите файл second.py в папку first.

```sh
ubuntu@ip-172-31-16-144:~$ mv second/second.py first
ubuntu@ip-172-31-16-144:~$ ls second/
ubuntu@ip-172-31-16-144:~$ ls first/
first.py  second.py
```

### 3. Удалите папку second.

```sh
ubuntu@ip-172-31-16-144:~$ rm -r second
ubuntu@ip-172-31-16-144:~$ ls
first
```

### 4. Переименуйте папку first в first_second.

```sh
ubuntu@ip-172-31-16-144:~$ mv first first_second
ubuntu@ip-172-31-16-144:~$ ls 
first_second
ubuntu@ip-172-31-16-144:~$ ls first_second/
first.py  second.py
```

### 5. Удалите папку first_second вместе с содержимым.

```sh
ubuntu@ip-172-31-16-144:~$ rm -r first_second/
ubuntu@ip-172-31-16-144:~$ ls
ubuntu@ip-172-31-16-144:~$ 
```

