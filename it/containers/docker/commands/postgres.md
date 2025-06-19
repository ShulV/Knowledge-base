#postgres #docker
## запуск контейнера
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

## Инициализация при запуске контейнера
#initdb #entrypoint
`docker-entrypoint-initdb.d.  - файл с действиями/скриптами
можно сделать монтирование и изменить скрипты инициализации
```bash
docker run --name test-pg-withdata -p 5555:5432 -e POSTGRES_PASSWORD=rootroot -d -v C:\tmp\sql:/docker-entrypoint-initdb.d postgres
```
P.S. скрипты упорядочены по названия и выполняются в том же порядке

## Монтирование директории с данными
#data #docker #postgres 
psql:
```bash
SHOW data_directory;
```
P.S. `/var/lib/postgresql/data` например такой результат

```bash
docker run --name test-pg-with-adata -p 5555:5432 -e POSTGRES_PASSWORD=rootroot -d -v /tmp/sql:/docker-entrypoint-initdb.d -v /tmp/sql/data:/var/lib/postgresql/data postgres
```
