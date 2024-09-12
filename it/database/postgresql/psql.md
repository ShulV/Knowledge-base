
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