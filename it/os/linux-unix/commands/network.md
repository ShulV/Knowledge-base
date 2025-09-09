
---
## Получить свой публичный ключ
#public #key
```bash
# дефолт
cat ~/.ssh/id_rsa.pub
# более современный и короткий
cat ~/.ssh/id_ed25519.pub
```
P.S. положить в ~/.ssh/authorized_keys на удаленном сервере к тому пользователю, к которому нужно будет подключаться

---
## Типы SSH-ключей
#terminal #command #ssh #network #rsa #ed25519 #security

**теория:**
**RSA, Ed25519 и ECDSA** - это различные алгоритмы шифрования, используемые для генерации SSH-ключей. Вот их основные отличия

- RSA - широко используемый и хорошо поддерживаемый алгоритм с хорошей производительностью.
- Ed25519 - современный и безопасный выбор с лучшей производительностью на современных устройствах (короткий ключ)
- ECDSA - использует более короткие ключи, хорошо подходит для ресурсоёмких сред и мобильных устройств.

---

## Подключение по SSH
#ssh #connect
```bash
ssh shulpov.v@50.249.14.205
```
shulpov.v - пользователь на тесте
50.249.14.205 - адрес сервера
порт по умолчанию - 22 (можно с флгом `-p` указать)


---

## Туннелирование запроса
#tunnel #proxy #ssh 

1) Проброс трафика на определенный порт на удаленном сервере
```bash
ssh -L 8085:localhost:443 admin@51.250.15.205
```

где:
51.250.15.205 - адрес сервера
443 - порт на удаленном сервере
8085 - локальный порт
флаг «‑L» - указывает на то, что нам необходимо открыть туннель и начать слушать порт

2) Проброс трафика на определенный адрес и порт на удаленном сервере
```bash
ssh -L 5432:postgres-db:5432:remote.server.address
```
где:
remote.server.address - адрес сервера
postgres-db - адрес postgres сервера
5432 (второй) - порт на удаленном сервере
5432 (первый) - локальный порт
флаг «‑L» - указывает на то, что нам необходимо открыть туннель и начать слушать порт




P.S. выжимка из более хардкорных мест
```
**-L** _порт:машина:порт_машины_

Определяет заданный порт на локальной (клиентской) машине который будет перенаправлен к заданной машине и порт на удаленной машине. Это реализовано путём назначения доменного подключения "прослушиваемому" _порту_ на стороне локальной машины и всякий раз, когда производится соединение на этот порт, оно будет перенаправлено через защищенный канал и произведено соединение к _порту_ _порт_машины_ удаленной машины. Перенаправление портов моет быть так же указано в файле конфигурации. Только суперпользователь может осуществлять перенаправление привилегированных портов. Адреса IPv6 могут быть указаны с альтернативным синтаксисом: _port/host/hostport_.
```

---

## Обратный туннель
#tunnel #reverse #proxy 
```bash
ssh -R 0.0.0.0:3001:127.0.0.1:3000 server.ru
```
где:
0.0.0.0:3001 - адрес и порт общего сервера
127.0.0.1:3000 - локальный адрес и порт
server.ru - адрес SSH сервера
флаг «‑R» - флаг открытия обратного туннеля

P.S.

---

## Proxy jump
#tunnel #jump #proxy 

прыжок через 1 сервер:
```bash
ssh -J <jump server> <remote server>
```
много серверов:
```bash
ssh -J <jump server1>,<jump server2>,<jump server3> <remote server>
```

---

## Запуск http-сервера
#http #httpd

```bash
python3 -m http.server --directory /var/www/html/ 8091
```

Команда  запускает простой HTTP-сервер, который служит файлами из текущей рабочей директории на порту 8091. Давайте разберем её подробнее:

1. **`python3`** – вызывает интерпретатор Python версии 3.x.
2. **`-m`** – флаг, указывающий, что модуль будет запущен как скрипт.
3. **`http.server`** – стандартный модуль Python, который предоставляет реализацию простого HTTP-сервера.
4. **`8091`** – номер порта, на котором будет работать сервер

P.S. является легким инструментом для временного обслуживания статичного контента (HTML-файлов, изображений, CSS и JavaScript).
Можно обращаться к файлам в указанном директории, например, из браузера.

НЕ ПОДДЕРЖИВАЕТСЯ OPTIONS - метод (были проблемы с загрузкой частями)

----
Лучше установить apache http-сервер, он более функциональный:
```bash
sudo npm install -g http-server
```
Запуск:
```bash
http-server -p 8091 -d /var/www/html
```
Что выводится при запуске:
```bash
Starting up http-server, serving ./

http-server version: 14.1.1

http-server settings: 
CORS: disabled
Cache: 3600 seconds
Connection Timeout: 120 seconds
Directory Listings: not visible
AutoIndex: visible
Serve GZIP Files: false
Serve Brotli Files: false
Default File Extension: none

Available on:
  http://127.0.0.1:8091
  http://192.168.30.15:8091
  http://10.8.0.30:8091
Hit CTRL-C to stop the server

...логи логи логи

```

----

## Настройка ssh-config
#ssh #config 
```bash
# PROJECT_1 - xmap
Host xmap_dev_jump
    User v.shulpov
    Hostname dev-xmap
    Port 25022

Host xmap_stage_app1
    User v.shulpov
    Hostname 198.12.21.20
    ProxyJump xmap_dev_jump

Host xmap_stage_app2
    User v.shulpov
    Hostname 198.12.21.21
    ProxyJump xmap_dev_jump

Host xmap_stage_db
    User v.shulpov
    Hostname 198.12.21.24
    ProxyJump xmap_dev_jumpp

# PROJECT_2

Host project2
    User admin
    Hostname 50.250.15.205
```

можно подключаться так:
```bash
# project 1 (через jump-сервер)
> ssh xmap_stage_app1
# project 2
ssh project2
```

---

## Проверки доступности и работоспособности сервиса на другом хосте
#ping #network 
```bash
shulpov.v@fedora:$ ping pg.company.team
PING pg.company.team (192.168.11.11) 56(84) bytes of data.64 bytes from pg.company.team (192.168.11.11): icmp_seq=1 ttl=64 time=0.645 ms64 bytes from pg.company.team (192.168.11.11): icmp_seq=2 ttl=64 time=0.677 ms64 bytes from pg.company.team (192.168.11.11): icmp_seq=3 ttl=64 time=0.536 ms
```
P.S.
проверяет доступность хоста путем отправки ICMP-запросов. Результаты показывают, что узел доступен и откликается быстро (менее миллисекунд)
#telnet #port #network

```bash
shulpov.v@fedora:~$ telnet pg.company.team 5432
Trying 192.168.11.11...
Connected to pg.soft-logic.team.
Escape character is '^]'.
```
P.S. 
попробовали установить прямое соединение с портом 5432 (стандартный порт PostgreSQL). Результат показал успешное установление соединения

#nslookup #network 
```bash
shulpov.v@fedora:$ nslookup pg.company.team
Server:        127.0.0.53
Address:    127.0.0.53#53
Name:   pg.company.team
Address: 192.168.11.11
```
P.S. 
Команда подтверждает разрешение DNS имени домена в правильный IP-адрес

---
## Проверка занят ли порт
#lsof #port #access #занят #http #ipv4 #tcp #listen
```bash
sudo lsof -i :1444
```
если свободен ничего не выведется, если занят, будет что-то вроде:
```bash
COMMAND   PID      USER   FD   TYPE  DEVICE SIZE/OFF NODE NAME
ssh     54821 shulpov.v    4u  IPv4 2559151      0t0  TCP localhost:marcam-lm (LISTEN)
```

---

