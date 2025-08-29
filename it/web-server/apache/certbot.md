#certbot #letsencrypt #encrypt #cert #certificate #https #tls
```bash
sudo dnf install epel-release
sudo dnf install certbot python3-certbot-apache

sudo certbot --apache -d spotic.ru
```

> P.S. Установит сертификат в апач сам

Перед этим нужно создать виртуальный хост в `/etc/httpd/conf.d` (например `default.conf`):
```
<VirtualHost *:80>    
	ServerName spotic.ru
	#    Redirect permanent "/" "https://spotic.ru/"  
</VirtualHost>
```