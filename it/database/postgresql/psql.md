
---

## Загрузить дамп в БД
#dump #command #terminal #psql #postgres
```bash
psql -U postgres -h localhost -d xmap_test -f xmap-dump-21-06-2024.sql
```

---

## подключение к БД
```bash
psql -U postgres -d  xmap-test
```

P.S при дефолт настройках
```bash
# зайти в psql под postgres юзером
sudo -U postgres psql

# зайти в psql в конкретную БД
psql -U viktor -d database_name
```

P.S. если сделать пользователя таким же, как в системе, то можно будет не вводить пароль, он будет тянутся оттуда. (Например, в viktor@fedora в линукс, viktor в postgresql)


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


---

##