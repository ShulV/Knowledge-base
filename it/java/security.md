
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
#spring #boot #tls #ssl #cert #trust
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

## Подключить https springboot
#https #ssl #tls #cert #certificate #keytool #pkcs #key #keystore

```bash
keytool -genkeypair \
  -alias test-cert-bvk \
  -keyalg RSA \
  -keysize 2048 \
  -storetype PKCS12 \
  -keystore keystore.p12 \
  -validity 3650 \
  -dname "CN=localhost, OU=keeper, O=sl, L=Local, S=Local, C=RU" \
  -ext "SAN=dns:localhost,ip:127.0.0.1"

```
- `-alias springboot`: имя для сертификата.
- `-keyalg RSA`: алгоритм ключа.
- `-keysize 2048`: размер ключа.
- `-storetype PKCS12`: формат хранилища.
- `-keystore keystore.p12`: имя файла хранилища (будет создан файл `keystore.p12`).
- `-validity 3650`: срок действия сертификата (10 лет).

application.yml
```yml
server.port=8443
server.ssl.key-store=classpath:keystore.p12
server.ssl.key-store-password=your-keystore-password
server.ssl.key-store-type=PKCS12
server.ssl.key-alias=test-cert-bvk
```

вытащить серт, чтобы положить его в браузер:
```bash
openssl pkcs12 -in keystore.p12 -clcerts -nokeys -out pub_cert.crt
```
можно вытащить `pem`, экспортировав прям из браузера (кликнуть на замочек в адресной строке)

