## Посмотреть количество коннектов на сервере
#connect #sql #stat #activity #datname #application #pool #connection

по коннектам к базам данных на сервере
```sql
SELECT count(*), datname FROM pg_stat_activity group by datname;
```

по коннектам приложений к базам
```sql
select application_name, COUNT(*) as count from pg_stat_activity group by application_name
```

общее количество текущий соединений:
```sql
SELECT sum(numbackends) FROM pg_stat_database;
```

максимальное количество коннектов:
```sql
SHOW max_connections;
```

P.S. допустимое кол-во коннектов также настраивается на уровне приложения!

---

