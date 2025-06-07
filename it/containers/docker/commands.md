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
#### вариант 1 (стандартный)
```bash
docker run -d -p 80:80 docker/getting-started
```
- `-d` - run the container in detached mode (in the background)
- `-p 80:80` - map port 80 of the host to port 80 in the container
- `docker/getting-started` - the image to use

#### вариант 2
```bash
docker run --network=host --env CLIENT_REDIRECT_URL=http://sp.mobcon.localhost/callback
```
1) `-e/--env` - установка переменной среды
2) `/--network` - все порты контейнера будут прослушиваться на хосте, даже те, которые не указаны в Dockerfile. Нужно, для того, чтобы программы внутри контейнера Docker выглядели так, будто они работают непосредственно на хосте с точки зрения сети. Не требуется прокидывать порт из локальной сети в контейнер.

#### другие параметры
- `-P` - запуск с рандомным портом
- -d - фоновый режим

P.S. 
- run скачает образ (pull), если его нет
- запускает в новом контейнере
---
## вывод контейнеров
#ps #all #list #container #docker 
```bash
docker ps -a
```

```bash
docker container ls -a
```
`-a` — флаг, который показывает все контейнеры (без этого флага `ps` выведет только работающие контейнеры)

---
## удалить контейнер
#rm #docker #container #remove #delete
```bash
docker rm <container_id>
```

---
## Изменить имя контейнера
#rename #docker #container
```bash
docker rename <oldname> <newname>
```
P.S. изменяет даже во время работы контейнера

---
## Посмотреть логи контейнера
#log #docker 
```bash
docker logs <container_name>
```

---
## Переход в оболочку контейнера
#terminal #sh #console #docker 
```bash
docker exec -it <container_name> /bin/sh
```
- `-i, --interactive` Keep STDIN open even if not attached
- `-t, --tty`  Allocate a pseudo-TTY
P.S. получаем полноценную интерактивную сессию Bash внутри контейнера с возможностью ввода команд и взаимодействия с ним, как будто находимся внутри самой операционной системы контейнера

---
## вывод образов
#image #show #list #docker 
```bash
docker images
```

```
docker image ls
```
P.S. у image больше параметров, но в представленном виде работает аналогично

---
## стянуть последнюю версию образа
#image #pull #docker 
```
docker pull <image_name>[:version]
```
P.S. по умолчанию версия - :latest

---

## управление контейнером
#container #docker 
```bash
docker start <container_id>
```

```bash
docker stop <container_id>
```

```bash
docker restart <container_id>
```

---

## монитрование
#mount #docker
### узнать тип монитрования
```bash
docker inspect <container_name>
```
P.S. выдает и много другой информации
### запуск с типом bind
#bind
```bash
docker run --name nginx-mount-bind -v /tmp/nginx:/usr/share/nginx/html -p 80:80 nginx
```
P.S. этот тип по умолчанию
P.S. /usr/share/nginx/html - папка по умолчанию, где nginx хранит файлы html страниц (как минимум основной и 50x)
### запуск с типом volume
#volume
```bash
docker run --name nginx-mount-volume -v nginx-volume-name:/usr/share/nginx/html -p 80:80 nginx
```

## postgres
#postgres #docker
### запуск контейнера
```bash
docker run -p 5555:5432 -d --name pg-17 -e POSTGRES_PASSWORD=rootroot postgres
```
`rootroot` - пароль для суперпользователя
`-e` - env переменнаяэ

## заходим в psql
#psql #docker
1) в ОС
```bash
docker exec -it pg-17 bash
```
2) в psql
```bash
psql -U postgres
```
в БД с названием `xmap`
```bash
psql -U postgres -d xmap
``` 

---


