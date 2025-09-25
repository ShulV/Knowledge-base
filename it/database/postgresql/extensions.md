#extension

тут должны лежать расширения
```bash
/usr/pgsql-17/share/extension/
```

## Postgis
#postgis #geography #coords #gis #latitude #longitude #extenstion
установка в систему
```bash
sudo dnf install -y postgresql-server postgresql-contrib postgis
```
> postgresql-server postgresql-contrib на всякий случай ещё раз (обычно уже установлено)

установка расширения (когда в директории уже лежит расширение `postgis.control`)
```sql
CREATE EXTENSION postgis;
```
узнать версию
```sql
SELECT PostGIS_Full_Version();
```

```sql
SELECT * FROM pg_available_extensions WHERE name = 'postgis';
```