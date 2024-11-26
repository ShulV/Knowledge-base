
---

## Запуск с игнорированием SSL
#ssl #https #tls #insecure

параметры
```java
-Dmaven.wagon.http.ssl.insecure=true -Dmaven.wagon.http.ssl.allowall=true
```

P.S. только в целях разработки и тестирования. Не для прода


---

## Явное указание корневого сертификата при запуске
#ssl  #tls #store #keystore #trust

```bash
-Djavax.net.ssl.trustStore=<path/to/store>
```


---

## Добавление CA в JVM
#ssl #tls #store #keytool #cacert #trust #crt #certificate 
```bash
sudo /home/shulpov.v/.jdks/openjdk-21.0.2/bin/keytool -importcert -trustcacerts -noprompt -cacerts -storepass changeit -file /home/shulpov.v/Загрузки/certs/xmap.crt -alias xmap
```

1. **`/home/shulpov.v/.jdks/openjdk-21.0.2/bin/keytool`** – путь к исполняемому файлу программы `keytool`, которая входит в состав JDK (Java Development Kit) и используется для управления сертификатами и ключами в Java.
2. **`-importcert`** – опция, указывающая, что нужно импортировать сертификат.
3. **`-trustcacerts`** – указывает, что при импорте сертификата должны быть проверены сертификаты из доверенного хранилища сертификатов (`cacerts`), чтобы убедиться, что они действительно заслуживают доверия.
4. **`-noprompt`** – эта опция отключает запросы подтверждения во время выполнения операции. То есть программа не будет запрашивать подтверждение действий у пользователя.
5. **`-cacerts`** – задает файл хранилища ключей, который будет использоваться для хранения сертификатов. В данном случае используется стандартный файл `cacerts`.
6. **`-storepass changeit`** – устанавливает пароль для доступа к хранилищу ключей. По умолчанию пароль для стандартного файла `cacerts` установлен как "changeit".
7. **`-file /home/shulpov.v/Загрузки/certs/xmap.crt`** – указывается путь к сертификату, который необходимо импортировать.
8. **`-alias xmap`** – имя (алиас), под которым этот сертификат будет сохранен в хранилище ключей.

---
