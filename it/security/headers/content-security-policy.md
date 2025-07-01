#security #policy #content #src #resources 
```java
/**  
 * Добавить Content-Security-Policy в ответ * Директивы, предоставляющие ограничения для загрузки ресурсов * default-src - общее по ресурсам, required * style-src - файлы CSS * img-src - файлы картинок и favicons * script-src - файлы JS, сценарии по onclick и XSLT stylesheets * font-src - шрифты, загруженные через @font-face * connect-src - загрузка ресурсов с помощью JS * frame-ancestors - указание предков, к-ые могут внедрить ресурс в страницу с помощью <frame>, <iframe>, <object>, <embed>  
 * object-src - источники для загрузки ресурсов ч/з <object, <embed>  
 * base-uri - ограничивает URI, к-ые можно использовать в <base>  
 * form-action - ограничивает URLs, к-ые указываются в форме в атрибуте action  
 * report-to - для указания эндпоинта, куда браузер будет сообщать о нарушениях */
 private void addCSPHeader(HttpServletResponse response) {  
    String headerValue = "default-src 'none'; style-src 'self';" +  
            " img-src 'self' data:" + imgSources + ';' +  
            " script-src 'self'; font-src 'self';" +  
            " connect-src 'self'" + connectSources + ';' +  
            " frame-ancestors" + frameAncestors + ';' +  
            " object-src 'none'; base-uri 'none'; base-uri 'none'; form-action 'self';" +  
            " report-to " + reportEndpoint + ';';  
    response.setHeader("Content-Security-Policy", headerValue);  
}
```

P.S. это можно сделать с помощью средств Spring Security, будет более красиво