## Wireguard
#nmcli #cli #wg #quick #wireguard #vpn #up #down

конфиги в `/etc/wireguard`

запуск
```bash
wg-quick up wg0
```

остановка
```bash
wg-quick down wg0
```

посмотреть запущенные ВПН:
```bash
wg-quick show
```

#list #wg #quick #wireguard
посмотреть все ВПН (просто посмотреть конфиги):
```bash
sudo ls /etc/wireguard/
```

добавить для графического интерфейса Network Manager
```bash
sudo nmcli connection import type wireguard file /etc/wireguard/wg0.conf
```

