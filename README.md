## Урок 7

### 1. Выбрать из домашней директории пользователя ubuntu файлы с расширением .py, название которых начинается на букву t.

```sh
ubuntu@ip-172-31-45-100:~$ ls | grep -e ^t.*\.py
test.py
```

### 2. Из всех файлов с расширением .py, расположенных в домашней директории пользователя ubuntu, выбрать строки, содержащие команду print, и вывести их на экран.

```sh
ubuntu@ip-172-31-45-100:~$ egrep -h  '([^#]*\s+|^)print\s*\(.*\)' *.py 
    print(i)
print("Hi there!")
print("Hello, world!")
print("Linear regression")
print("Linear regression")
print("test")

```

### 3. Из результатов работы команды uptime выведите число дней, которое система работает без перезагрузки.

Проверено на 
uptime from procps-ng 3.3.10
Для aws не накопилось время

```sh
ubuntu@ip-172-31-45-100:~$ uptime -V
uptime from procps-ng UNKNOWN
ubuntu@ip-172-31-45-100:~$ uptime | sed -e 's/^.* up \+\(\(\([0-9]\)*\) days, \)*\([^,]*\)*,.*/\2/' | sed -e 's/^$/0/'
0
```
