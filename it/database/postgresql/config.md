
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

обычно меняем:
1)
```
host    all             all             127.0.0.1/32            ident
```
на
```
host    all             all             127.0.0.1/32            md5
```
2)
```
host    all             all             ::1/128                 ident
```
на
```
host    all             all             ::1/128                 md5
```

И нужно перезапустить постргрес!

---

