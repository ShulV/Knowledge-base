
---
## chattr и lsattr
#неизменяемый #флаг

```bash
chattr опции [оператор][атрибуты] файлы
```

снять флаг неизменяемости файла
```bash
sudo chattr -i /srv/xmap-api/xmap-api.jar
```

добавить флаг неизменяемости файла
```bash
sudo chattr +i /srv/xmap-api/xmap-api.jar
```

P.S. даже под SUDO не получится изменять файлы. Нужен, чтобы случайно не удалить что-то важное :)

---

## Копирование между серверами
#copy #scp
```bash
scp /home/shulpov.v/IdeaProjects/application/xmap/build/libs/xmap-3.95-SNAPSHOT.jar shulpov.v@50.249.14.205:/home/shulpov.v/xmap.jar
```

---

##

