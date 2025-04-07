## systemctl docker сервис
```bash
sudo systemctl status docker
sudo systemctl start docker
# автоматический запуск при загрузке системы
sudo systemctl enable docker
```

---
## запуск контейнера
#run #docker #container
```bash
docker run --network=host --env CLIENT_REDIRECT_URL=http://sp.mobcon.localhost/callback
```
1) `-e/--env` - установка переменной среды
2) `/--network` - все порты контейнера будут прослушиваться на хосте, даже те, которые не указаны в Dockerfile. Нужно, для того, чтобы программы внутри контейнера Docker выглядели так, будто они работают непосредственно на хосте с точки зрения сети. Не требуется прокидывать порт из локальной сети в контейнер.


---
## вывод контейнеров
#ps #all #list #container #docker 
```bash
docker ps -a
```
`-a` — флаг, который показывает все контейнеры (без этого флага `ps` выведет только работающие контейнеры)

---
## удалить контейнер
#rm #docker #container
```bash
docker rm <container_id>
```

---
## Изменить имя контейнера
#rename 
```bash
docker rename <oldname> <newname>
```
P.S. изменяет даже во время работы контейнера

---
## Посмотреть логи контейнера
#log 
```bash
docker logs <container_name>
```

---
