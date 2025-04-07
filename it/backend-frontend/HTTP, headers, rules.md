
## Согласование формата данных между клиентом и сервером
#client #server #content-type #header #http #headers #json #xml #status_code #status406  #not_acceptable
1. **Client Preference** (Предпочтения клиента): Клиент указывает предпочтительный формат (форматы) данных с помощью заголовка **HTTP** **header**:
    
    **Accept header**: Определяет типы медиа, которые может обрабатывать клиент, например, `Accept: application/json, application/xml.`  
    **Content-Type header**: Определяет формат данных, отправляемых в теле запроса, например, `Content-Type: application/json.`
    
2. **Server Response** (Ответ сервера): Сервер анализирует заголовок Accept header и определяет наилучший формат, который он может предоставить. Если поддерживается несколько форматов, сервер выбирает наиболее подходящий из них на основе приоритета.
    
3. **Response** (Ответ): Сервер отправляет ответ в согласованном формате вместе с заголовком `Content-Type,` указывающим тип носителя,  
    например `Content-Type: application/json.`
    

##### Types of Content Negotiation (Типы переговоров по содержимому)

1. **Server-Driven Negotiation** (Переговоры, управляемые сервером): Сервер принимает решение о формате ответа на основе заголовка `Accept` от клиента.
    
2. **Client-Driven Negotiation** (Переговоры, управляемые клиентом): Клиент запрашивает определенные форматы через параметры запроса, например,`?format=json`.
    
3. **Agent-Driven Negotiation**: Посредническое программное обеспечение или прокси согласовывает формат содержимого.

**Пример**: Предположим, клиент отправляет микросервису следующий запрос:

```bash
GET /users HTTP/1.1   Accept: application/json
```

Если сервер поддерживает JSON, он отвечает на запрос:

```bash
HTTP/1.1 200 OK Content-Type: application/json{   "id": 1,   "name": "Shivam Srivastava" }
```

В противном случае. сервер возвращает ответ:

```bash
HTTP/1.1 406 Not Acceptable
```

---

## Сессии и куки
#session #http #set-cookie #cookie #header #headers #insecure 

Заголовок ответа для установки куки:
```
Set-Cookie: <cookie-name>=<cookie-value>
```

**Опции:**
1)
```
expires=<date>
```
2)
```
max-age=<number>
```
3)
```
domain=<domain-value>
```
4)
```
secure
```
P.S.
The `secure` attribute does not safeguard [Cookies](https://http.dev/cookies "Cookies") against programs that can read the client’s physical hard drive. Also, access to the cookie is possible using _JavaScript_ if the `HttpOnly` attribute is not included.
5)
```
HttpOnly
```
When the `HttpOnly` attribute is set, _JavaScipt_ applications do not have raw access to the cookie’s data. The cookie can still be sent but it cannot be accessed through the document properties.
6)
```
SameSite=<SameSite-value>
```

**Пример:**
```
Set-Cookie: sid=14A52; max-age=3600
```