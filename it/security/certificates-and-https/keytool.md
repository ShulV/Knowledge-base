## Добавить серт в cacert (в JVM)
#cacerts #jvm #jre

#### crt
```bash
keytool -import -trustcacerts -keystore ~/Library/Java/JavaVirtualMachines/corretto-21.0.5/Contents/Home/lib/security/cacerts \
   -storepass changeit -noprompt -alias mycert -file ~/development/keycloak-26.2.1/bin/spotic_server.crt
```
#### pem
```bash
keytool -importcert -file ~/development/keycloak-26.2.1/bin/keycloak_chain_cert.pem -alias keycloak_chain_cert -keystore ~/Library/Java/JavaVirtualMachines/corretto-21.0.5/Contents/Home/lib/security/cacerts
```

---
## Проверить существование сертификата в cacert
#list #cacert
```bash
keytool -list -v -keystore ~/Library/Java/JavaVirtualMachines/corretto-21.0.5/Contents/Home/lib/security/cacert | grep keycloak_cert
```

где keycloak_cert - алиас сертификата

---

## Удалить сертификат из cacert
#delete #remove #cacert 
```bash
keytool -delete -alias mycert -keystore ~/Library/Java/JavaVirtualMachines/corretto-21.0.5/Contents/Home/lib/security/cacerts -storepass changeit
```