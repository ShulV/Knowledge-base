## Температура ЦП, шин, интерфейсов
#monitoring #temperature
```python
watch -n 2 sensors
```
температуры различных компонент, инфа обновляется каждые 2 секунды

---
## Оперативная память
#ram #mem #free #buffer #cache #monitoring
```bash
[victor@r1027047 ~]$ free -h
               total        used        free      shared  buff/cache   available
Mem:           764Mi       260Mi       269Mi       2.0Mi       353Mi       504Mi
Swap:          1.0Gi        23Mi       1.0Gi
```

`-h` - human вывод

---
## Память диска
#disk #mem #monitoring
```bash
df -h
Filesystem      Size  Used Avail Use% Mounted on
devtmpfs        4.0M     0  4.0M   0% /dev
tmpfs           383M     0  383M   0% /dev/shm
tmpfs           153M  4.1M  149M   3% /run
/dev/sda1        21G  2.5G   18G  13% /
tmpfs            77M     0   77M   0% /run/user/1000
```

----
## Процессор
#processor #thread #core #socket #cpu #monitoring
полная информация о процессоре:
```bash
lscpu
```
красиво и минималистично:
```bash
lscpu | grep -E '^Thread|^Core|^Socket|^CPU\('
```
вывод:
```
CPU(s):                4
Thread(s) per core:    2
Core(s) per socket:    2
Socket(s):             1
```
P.S. 
логические ядра/потоки/виртуальные ядра - 4, 
потоков (логических ядер) на физическое ядро - 2 (Hyper-threading), 
физических ядер - 2, 
сокетов (процессорных разъемов) - 1

---
