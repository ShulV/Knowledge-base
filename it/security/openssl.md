
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

