## Сертификат для angular проекта на macos (и не только)

- Установите `mkcert`: 
    
    ```bash
    brew install mkcert
    brew install nss
    ```

- Создайте корневой сертификат и установите его:

```bash
victor@MacMini ~ % mkcert -install 
The local CA is already installed in the system trust store! 👍
The local CA is now installed in the Firefox trust store (requires browser restart)! 🦊
```

 P.S. создат доверенный для системы CA, пропишет его в системе, для firefox, (chrome берет из системы автоматом).
 Далее серты, создаваемые с помощью `mkcert`
 будут подписывать этим CA.
 
```bash
# для macos создается тут: /Users/victor/Library/Application Support/mkcert
-r--------   1 victor  staff rootCA-key.pem
-rw-r--r--   1 victor  staff rootCA.pem
```

- Сгенерируйте сертификаты для домена `localhost`:
    
    ```bash
    mkcert localhost
    ```
    
- Добавьте полученные файлы сертификата и ключа в конфигурацию Angular CLI

P.S. замок в браузере больше не красный! https работает!

---

```bash
mkcert -cert-file spotic_server.crt -key-file spotic_private.key localhost 127.0.0.1 ::1
```


так сразу создается .p12  с нужным названием (ключ и серт тут можно не указывать, это для временного хранения)
```bash
mkcert -pkcs12 -cert-file spotic_server.crt -key-file spotic_private.key -p12-file spotic_container.p12 localhost 127.0.0.1 ::1
```