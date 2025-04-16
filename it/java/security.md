
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

----

## Где хранятся корневые серты в linux:
#ca
```
/etc/pki/ca-trust/source/anchors/
```

---
