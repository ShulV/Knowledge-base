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
