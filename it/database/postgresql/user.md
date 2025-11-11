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
