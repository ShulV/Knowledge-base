## Текущее состояние
#timezone #get #status #check #tz #time #clock
```bash
timedatectl status
```

```bash
               Local time: Пн 2025-09-22 11:15:57 MSK
           Universal time: Пн 2025-09-22 08:15:57 UTC
                 RTC time: Пн 2025-09-22 08:15:57
                Time zone: Europe/Moscow (MSK, +0300)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no

```

## Список таймзон
#list #timezone #tz #time #clock
```bash
timedatectl list-timezones
```

```bash
Africa/Abidjan
Africa/Accra
Africa/Addis_Ababa
Africa/Algiers
Africa/Asmara
Africa/Asmera
...
```

## Изменить таймзону
#change #timezone #tz #time #clock
какие есть
```bash
timedatectl `list-timezones`
```
изменить
```bash
timedatectl set-timezone <time_zone>
```