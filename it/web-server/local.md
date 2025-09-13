#web-server #server #python #static #раздача_статики
## Запуск http-сервера для раздачи статики
#http #httpd
```bash
python3 -m http.server --directory /var/www/html/ 8091
```
Команда  запускает простой HTTP-сервер, который служит файлами из текущей рабочей директории на порту 8091. Давайте разберем её подробнее:

1. **`python3`** – вызывает интерпретатор Python версии 3.x.
2. **`-m`** – флаг, указывающий, что модуль будет запущен как скрипт.
3. **`http.server`** – стандартный модуль Python, который предоставляет реализацию простого HTTP-сервера.
4. **`8091`** – номер порта, на котором будет работать сервер

P.S. является легким инструментом для временного обслуживания статичного контента (HTML-файлов, изображений, CSS и JavaScript).
Можно обращаться к файлам в указанном директории, например, из браузера.

НЕ ПОДДЕРЖИВАЕТСЯ OPTIONS - метод (были проблемы с загрузкой частями)

----
Лучше установить apache http-сервер, он более функциональный:
```bash
sudo npm install -g http-server
```
Запуск:
```bash
http-server -p 8091 -d /var/www/html
```
Что выводится при запуске:
```bash
Starting up http-server, serving ./

http-server version: 14.1.1

http-server settings: 
CORS: disabled
Cache: 3600 seconds
Connection Timeout: 120 seconds
Directory Listings: not visible
AutoIndex: visible
Serve GZIP Files: false
Serve Brotli Files: false
Default File Extension: none

Available on:
  http://127.0.0.1:8091
  http://192.168.30.15:8091
  http://10.8.0.30:8091
Hit CTRL-C to stop the server

...логи логи логи

```