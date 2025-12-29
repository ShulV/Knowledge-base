## Температура ЦП, шин, интерфейсов
#monitoring #temperature
```python
watch -n 2 sensors
```
температуры различных компонент, инфа обновляется каждые 2 секунды

---
## Оперативная память
#### общая таблица
#ram #mem #free #buffer #cache #monitoring
```bash
[victor@r1027047 ~]$ free -h
               total        used        free      shared  buff/cache   available
Mem:           764Mi       260Mi       269Mi       2.0Mi       353Mi       504Mi
Swap:          1.0Gi        23Mi       1.0Gi
```

`-h` - human вывод

#### Сколько оперативки жрут конкретные java приложения
#ram #mem #free #buffer #cache #monitoring #java
```bash
printf "%-7s %-8s %-8s %-8s %-25s %s\n" \
"PID" "RAM(MB)" "Xms(MB)" "Xmx(MB)" "WORKDIR" "APP"

pgrep -a java | while read -r pid args; do
    rss=$(ps -o rss= -p "$pid")
    mem_mb=$(printf "%.1f" "$(echo "$rss / 1024" | bc -l)")

    cwd_full=$(readlink -f /proc/$pid/cwd)
    cwd=$(echo "$cwd_full" | awk -F/ '{n=NF; if(n>3) print $(n-2)"/"$(n-1)"/"$n; else print $0}')

    norm() {
        val="$1"
        if [[ "$val" =~ [gG]$ ]]; then
            echo $(( ${val%[gG]} * 1024 ))
        elif [[ "$val" =~ [mM]$ ]]; then
            echo $(( ${val%[mM]} ))
        else
            echo "$val"
        fi
    }

    xms=$(echo "$args" | grep -oE '\-Xms[0-9]+[mMgG]' | sed 's/-Xms//')
    xmx=$(echo "$args" | grep -oE '\-Xmx[0-9]+[mMgG]' | sed 's/-Xmx//')

    [ -z "$xms" ] && xms="-" || xms=$(norm "$xms")
    [ -z "$xmx" ] && xmx="-" || xmx=$(norm "$xmx")

    # Находим последний «чистый» JAR (не начинающийся с '-') 
    jars=($(echo "$args" | grep -oE '[^ ]+\.jar' | grep -v '^-'))
    if [ ${#jars[@]} -gt 0 ]; then
        app=$(basename "${jars[-1]}")
    else
        app=$(echo "$args" | awk '{
            for(i=1;i<=NF;i++)
                if($i !~ /^-/ && $i !~ /\// && $i !~ /=/ && $i !~ /\.jar$/)
                    { print $i; exit }
        }')
        [ -z "$app" ] && app="-"
    fi

    printf "%-7s %-8s %-8s %-8s %-25s %s\n" \
        "$pid" "$mem_mb" "$xms" "$xmx" "$cwd" "$app"
done | sort -k2 -nr
```

P.S. не разбирался с запросом, но выводим в целом норм. (админку у нас на томкате например, не выводил, не финальный идеальный скрипт)

#### Группировка по имени процесса (сортировка по RAM)
#ram #mem #free #buffer #cache #monitoring #java
```bash
ps -eo comm,rss \
  | awk '{mem[$1]+=$2} END {for (i in mem) printf "%s %.2f\n", i, mem[i]/1024}' \
  | sort -k2 -nr
```


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

## Данные о перезапусках сервера
#reboot #server
```bash
last reboot
```