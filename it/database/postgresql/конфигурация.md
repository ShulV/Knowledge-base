
---
## postgresql.conf
```
/data/postgresql.conf
```
P.S. в файле можно настроить БД, есть настройки по логированию и ротации логов

---
## pg_hba

TYPE  DATABASE        USER            ADDRESS                 METHOD
#"local" is for Unix domain socket connections only
local   all                       all                                                   trust

---

