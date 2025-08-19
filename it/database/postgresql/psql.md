
---

## Загрузить дамп в БД
#dump #command #terminal #psql #postgres
```bash
psql -U postgres -h localhost -d xmap_test -f xmap-dump-21-06-2024.sql
```
``-U _`username`_``  
``--username=_`username`_``

``-d _`dbname`_``  
``--dbname=_`dbname`_``

``-h _`hostname`_``  
``--host=_`hostname`_``

``-p _`port`_``  
``--port=_`port`_``

``-f _`filename`_``  
``--file=_`filename`_``
Write all query output into file _`filename`_, in addition to the normal output destination.

``-o _`filename`_``  
``--output=_`filename`_`` 
Put all query output into file _`filename`_. This is equivalent to the command `\o`.


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
## List all databases
```bash
\l
```

---

## List database tables 
```
\dt
```

---

## Describe a table 
```
\d
```

```
\d <table-name>

// example
\d tutorials
```

---

## List users and their roles
```
\du
```


## Залить дамп из SQL файла
```bash
psql -U viktor xmap < /home/shulpov.v/xmap-2024-11-13T00\:01\:01.sql
```

## Залить дамп из DMP файла
```bash
sudo -u postgres psql -h 127.0.0.1 -p 5432 -U my_user -W my_db < by_db_14-07-2025.dmp
```

---

## Узнать какие есть БД
#all #db #postgres #list #role #psql
если пользователь - postgres
```bash
sudo -u postgres psql -l
```

P.S. так будет проверяться под пользователем с именем текущего юзера в ОС (например, в viktor@some-server пользователь системы - viktor, команда сделает что-то такое: sudo -u viktor psql -l и если пользователя не будет, вернет ошибку)
```bash
psql -l
```
пример ошибки
```bash
psql: error: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: FATAL:  role "viktor" does not exist

```

---

## Создать нового пользователя
#create #user #role 
```bash
CREATE USER app_admin WITH PASSWORD 'password123';
```

## Дать пользователю все привилегии на БД
#grant #privileges #user #all
```sql
GRANT ALL PRIVILEGES ON DATABASE app_database TO app_admin;
```

на все таблицы
```sql
GRANT ALL ON ALL TABLES IN SCHEMA public TO app_admin;
```

на схему
```sql
GRANT ALL ON SCHEMA public TO app_admin;
```

---
## Изменить пароль
#change #password #alter

```sql
ALTER USER user_name WITH PASSWORD 'new_password';
```

---
## Посмотреть настройки БД
```bash
SHOW all;
```

## Посмотреть директорию с данными БД
#directory #data #postgres
```bash
SHOW data_directory;
```
P.S. `/var/lib/postgresql/data` например такой результат

---

## Поднять значение итератора в sequence
#up #sequence #iterator
```sql
SELECT setval('my_sequence', currval('my_sequence') + 1000);
```

select nextval ( 'client_login_id_seq' )

---

## Индекс на колонку на уникальность
#unique #constraint #index #idx
```sql
create unique index if not exists  
    client_workspace_role_code_idx on client_workspace_role (code);
```

---

