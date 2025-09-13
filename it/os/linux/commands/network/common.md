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
