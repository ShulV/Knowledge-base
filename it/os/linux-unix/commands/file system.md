
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

## Информация о файлах и каталогах
#ls #la #command #linux
```bash
ls -la
```

Пример вывода:
```bash
drwxr-xr-x. 1 shulpov.v shulpov.v    180 сен 12 14:55 .  
drwxr-xr-x. 1 root      root         554 сен  5 16:09 ..  
-rw-r--r--. 1 shulpov.v shulpov.v   4314 сен 12 14:55 application.yml  
-rw-r--r--. 1 shulpov.v shulpov.v    953 янв 26  2024 config.xml  
drwxr-xr-x. 1 shulpov.v shulpov.v    160 июн  7 09:23 log  
drwxr-xr-x. 1 shulpov.v shulpov.v   1038 сен 12 15:00 logs  
drwxr-xr-x. 1 shulpov.v shulpov.v      0 мая  2 16:59 reports
```

P.S. права на чтение/запись/запуск... , пользователь и группа и т.д.

---
## Найти каталоги, начинающиеся на опред. букву
#regexp #template #ls 
```bash
ls -ld /usr/bin/p*
```
- `-l` — показывает подробную информацию о файлах и папках (размер, права доступа, дата модификации и т.п.).
- `-d` — показывает только сами директории, без их содержимого.
- p*` — маска шаблона, означающая, что нужно выбрать все элементы, названия которых начинаются с буквы "p".
---

## Найти строки, включающие подстроку
#grep #command #search

```bash
grep "operation_id = '1092222" log_file.txt
```


## Найти строки в файлах, где встречается подстрока
#grep #search #recusive #substring #file

```bash
grep -Ri 'linux' /home/user
```
- `-R`: Рекурсивный поиск. Поиск осуществляется во всех файлах в текущей директории и её поддиректориях.
- `-i`: Игнорирование регистра. Поиск ведётся без учёта регистра символов.
- `-l`: Только вывод номеров строк. Не выводит сами строки, содержащие совпадения.
- `-n`: Не показывать совпадающие строки.
- `-c`: Показывать количество совпадений.
- `-v`: Показывать только непересекающиеся строки.

---

## Найти самые крупные файлы
#monitoring 
Найдет самые большие по размеру директории в текущей директории и выведет всё.
```bash
du -ah | sort -rh | head -n 10
```

P.S. удобно искать утечки :)

----

#### Разбить файл на несколько равных по размеру
#linux #command #split #file #separate
```bash
split -n 8 ./bank.log
```


---

## Очистить файл
#clear #file #command #linux #input
перезаписать пустотой
```bash
> filename
```

---

## Вывод последней строки
#tail #last #end
```bash
sudo tail -n 1 /srv/xmap-api/logs/some.log
```

