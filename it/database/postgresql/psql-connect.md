
---
## Разница флагов -u и -U
- **Флаг `-u`** используется командой `sudo` для временной смены текущего пользователя Linux/Unix.
- **Флаг `-U`** используется командой `psql` для указания пользователя PostgreSQL, от имени которого производится подключение к базе данных.

----
## Выполнить psql-команду,  из терминала ОС
```bash
sudo -u postgres psql -c "\du";
```

-c _`command`
--command=_`command`

---

## Подключение к psql под postgres пользователем
```bash
sudo -u postgres psql
```

---
## подключение к БД
```bash
psql -U postgres -d  xmap-test
```

P.S при дефолт настройках
```bash
# зайти в psql под postgres юзером
sudo -u postgres psql

# зайти в psql в конкретную БД
psql -U viktor -d database_name
```

P.S. если сделать пользователя таким же, как в системе, то можно будет не вводить пароль, он будет тянутся оттуда. (Например, в viktor@fedora в линукс, viktor в postgresql)

```bash
psql -h <host> -p <port> -U <username> -W <password> <database>
```

---
