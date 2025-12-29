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

удалить это соединение
```bash
sudo nmcli connection delete wg0
```

#### связь с systemctl

```bash
systemctl stop wg-quick@wg0
systemctl start wg-quick@wg0
systemctl restart wg-quick@wg0
systemctl enable wg-quick@wg0
```

#### пример конфига
```
[Interface]
PrivateKey = oGMmBl1bP4pLhDqf8Tqt+opsMucZZoAPy/2MSgx6NHk=
Address = 10.8.0.30/24
DNS = 1.1.1.1
[Peer]
PublicKey = DbbPCGOpPn0CuvphVsCpldXQ7wnMzRDjJWXunYCua2M=
PresharedKey = Z+sFbxb5mAEzEL5xwJf/6hK4mMmS8zmST7BSsJNYwyk=
AllowedIPs = 51.250.15.206, 62.84.127.19, 95.217.0.16
PersistentKeepalive = 0
Endpoint = 51.250.26.232:51820

```
- `Address` — «мой внутренний VPN‑IP».
- `Endpoint` — «куда в интернет стучаться, чтобы попасть к VPN‑серверу».
- `AllowedIPs` — адреса, на которые обращаться через VPN

P.S. настройка `DNS` может перекрывать "офисный" DNS

