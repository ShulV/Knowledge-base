## Добавление swap
#swap #mem #memory #allocate #fallocate #buffer #cache
P.S. на сервере с 1 гб оперативки не удается установить пакеты
```bash
[root@r1027047 victor]# dnf install mc
Killed
```
команды:
```bash
sudo fallocate -l 1G /swapfile
```
создается файл /swapfile
размер = 1 гб
выделяет место на диске (без заполнения нулями)

все юзеры могут писать и читать в своп, но владелец root
```bash
chmod 600 /swapfile
```

```bash
[root@r1027047 victor]# ls -la /swapfile

-rw-------. 1 root root 1073741824 Aug 13 17:31 /swapfile
```

```bash
[victor@r1027047 ~]$ sudo mkswap /swapfile
```

Отформатировали файл как файл подкачки. Активировался сразу. Без метки, но с идентификатором.
```
mkswap: /swapfile: warning: wiping old swap signature.

Setting up swapspace version 1, size = 1024 MiB (1073737728 bytes)

no label, UUID=b35990c5-5baa-4a5d-b326-db8b54541717
```

активация свопа
```bash
sudo swapon /swapfile
```
проверка работы свопа

```bash
[victor@r1027047 ~]$ sudo swapon --show

NAME      TYPE  SIZE USED PRIO
/swapfile file 1024M   0B   -2
```

P.S. `/etc/fstab` описывает файловую систему и разделы

#tee
команда добавляет текст в конец файла из потока ввода
```bash
tee -a /some-path
```
```ctrl+D``` - выйти из потока ввода

```bash
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

----
## Создать пользователя
#create #user 
```bash
sudo adduser newusername
%% или %%
sudo useradd newusername
```
----
## Сменить пароль
#password #passwd #change
```java
//текущему
passwd
//другому пользователю
passwd username
```

---

