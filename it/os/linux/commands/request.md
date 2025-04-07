## curl
#curl #linux #request #console #terminal #command
- `-X, --request` определяет метод запроса, например, `curl -X POST url`

- `-d, --data` определяет тело запроса в виде строки в PUT и POST-запросах. Используйте `@` для извлечения данных из файла
2 варианта одного и того же (-d):
```bash
curl --request POST 'https://api.mts.ru/token?grant_type=client_credentials' -H 'Authorization: ••••••'
```

```bash
curl --request POST 'https://api.mts.ru/token' -d 'grant_type=client_credentials' -H 'Authorization: ••••••
```

P.S. в postman это таб 'Params'

- `-H, --header` определяет заголовок запроса, например, `curl -H "Authorization: my-secret-token" url`

- `-u, --user` аутентификационные данные для стандартной авторизации
 -u флаг создает заголовок Authorization со значением base64(login:password)
 (можно дополнительно указазать --basic, --digest... Но обычно можно не указывать)
 
- `-O` сохраняет тело запроса в файл

- `-i, --show-headers` показывает полный ответ, включая заголовки

- `-k, --insecure` отключает проверку сертификата SSL/TLS при установлении защищенного соединения