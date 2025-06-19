#compose #docker 

---
## запуск
```bash
docker compose up
```

---
## логи контейнеров
#log #docker #compose
```bash
docker compose logs --follow
```

---

## Пересоздание образа при запуске
```bash
docker build -t backend-docker .
docker compose up --force-recreate
```

`-t` - имя образа
`--force-recreate`  удаляет старую версию контейнера перед запуском даже если там не было изменений

---

