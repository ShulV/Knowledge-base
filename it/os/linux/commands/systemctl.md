
---
## Получить все сервисы
#list #service #unit #systemctl
```bash
systemctl list-units --type=service
```

---
## Запуск, остановка, статус сервиса
#systemctl #start #stop #status
```bash
systemctl start xmap
systemctl stop xmap
systemctl status xmap
```
---
## Посмотреть поток вывода программы за промежуток времени
#systemctl #journal #journalctl #sout 

```bash
sudo journalctl -u xmap-api.service --since "10 minutes ago"
```
---

