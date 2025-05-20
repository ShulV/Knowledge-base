
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
## Connection APIs in java
#keystore #truststore #keymanager #ssl #sslcontext #trustmanager
- Some want you to provide keystore and truststore `java.security.KeyStore` instances.
- Some want you to provide `javax.net.ssl.KeyManager` and `javax.net.ssl.TrustManager` instances.
- Some want you to provide a `javax.net.ssl.SSLContext` instance.

low-level settings:
`java.security` or `java.net.ssl` packages

Для RestTemplate - ClientHttpRequestFactory

настройка для разных случаев в spring boot
https://spring.io/blog/2023/06/07/securing-spring-boot-applications-with-ssl

---
## Настройка ssl/tls через конфиг spring boot

```yml
server: 
. ssl: 
	key-alias: “server”
	key-password: “keysecret”
	key-store: "classpath:server.p12"
	key-store-password: "storesecret" 
	client-auth: NEED
```

```yml
spring: 
. ssl: 
.   bundle: 
      jks: 
        web-server: 
          key: 
            alias: "server"
            password: “keysecret”
            keystore: 
              location: "classpath:server.p12"
              password: "storesecret" 
server: 
  ssl: 
    bundle: “web-server” 
    client-auth: NEED
```

P.S. технически делают одно и то же, первый более новый вариант

---
