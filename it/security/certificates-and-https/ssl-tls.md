
---
## Запрос через curl с использованием сертификата
#curl #p12 #insecure #cert #certificate #сертификат
```bash
curl --insecure --cert-type P12 --cert /path-to/your-file.p12:the-password https://your-host.com/endpoint
```

---

## Настройка сертификата в postman
#postman #p12 #cert #certificate #сертификат
Postman Settings:

```java
Postman->preferences->General
SSL certificate verification OFF
```

Postman Certs:

```java
Postman->preferences->Certificates
Client Certificates:


Host yourhost.com
CRT file
Key file
PFX file  /path-to-file/CertificateFile.p12  
Passphrase your-file-password
```

---

##