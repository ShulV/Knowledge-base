	## Экспортировать цепочку сертификатов из браузера
#chain #browser #export #cert #certificate 
```bash
openssl s_client -showcerts -verify 5 -connect localhost:8443 </dev/null | tee output.txt
```

P.S. можно скопировать цепочку из output.txt, begin-end часть.
Поместить ее в новый pem файл

---

#openssl #pkcs7 #p7b #x509 #pem

p7b бинарный (нечитаемый), переводим в pem, его можно посмотреть (будет видно начало первого сертификата и конец, также со вторым. BEGIN/END)
```bash
openssl pkcs7 -inform der -in ~/tlscaroot.p7b -print_certs -out ~/mts.pem
```

посмотреть инфу по сертификатам PEM в терминале:
```bash
openssl x509 -in ~/mts.pem -text -noout
```

Если их нужно разделить на разные файлы, это можно сделать вручную в текстовом редакторе.

---

## Сгенерировать самоподписанный сертификат
#openssl #cert #certificate #key #cer #create #generate
```bash
openssl req -x509 -newkey rsa:2048 -nodes -keyout server.key -out server.cer -days 3650 -subj "/C=RU/ST=Moscow/L=Moscow/O=My Company/CN=localhost"
```
  
Эта команда создаст два файла:

- `server.key`: приватный ключ RSA.
- `server.cer`: публичный сертификат X.509.

X.509 используется для идентификации сервера и обеспечения безопасного соединения через протокол TLS/SSL. Обычно такие сертификаты выдаются центрами сертификации (CA), такими как Let's Encrypt, DigiCert и другие. Однако для разработки и тестирования можно создать самоподписанный сертификат.

---

## PEM формат -> PKCS#8
#private #key #binary #pkcs 
PKCS#8 — это стандартизированный формат хранения ключей. В отличие от традиционного формата PEM, который использует заголовки и концевики (`-----BEGIN PRIVATE KEY-----`), формат PKCS#8 хранит ключи в бинарной форме. Приватный ключ в формате PKCS#8 часто используется в веб-серверах для работы с HTTPS.

```bash
openssl pkcs8 -topk8 -inform PEM -in server.key -outform PEM -nocrypt -out server.pkcs8
```

---

## Генерация .p12 (.pfx) контейнера
1) Эта команда создаст файл private.key, содержащий закрытый ключ RSA длиной 2048 бит и сертификата.
```bash
openssl req -newkey rsa:2048 -nodes -keyout private.key -x509 -out certificate.cer
```
P.S. советуют указывать CN=localhost
2) создать контейнер с помощью закрытого ключа и сертификата
```bash
openssl pkcs12 -export -out certificate.pfx -inkey private.key -in certificate.cer
```
При выполнении этой команды вам будет предложено ввести пароль для защиты контейнера PFX

----
## Получить корневой сертификат сервиса по адресу и порту
```python
openssl s_client -connect localhost:8090 -showcerts </dev/null 2>/dev/null|openssl x509 -outform PEM > 
./root_ca.crt
```

--- 

#openssl #pkcs7 #p7b #x509 #pem

p7b бинарный (нечитаемый), переводим в pem, его можно посмотреть (будет видно начало первого сертификата и конец, также со вторым. BEGIN/END)
```bash
openssl pkcs7 -inform der -in ~/tlscaroot.p7b -print_certs -out ~/mts.pem
```

посмотреть инфу по сертификатам PEM в терминале:
```bash
openssl x509 -in ~/mts.pem -text -noout
```

Если их нужно разделить на разные файлы, это можно сделать вручную в текстовом редакторе.


---

