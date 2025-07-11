#security #policy #content #src #resources 

## low level
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

## spring security
P.S. это можно сделать с помощью средств Spring Security, будет более красиво

```java
@Configuration  
@EnableWebSecurity  
public class WebSecurityConfig {  
  
	@Bean  
	public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {  
		http  
			.headers(headers -> headers  
				.contentSecurityPolicy(csp -> csp  
					.policyDirectives("default-src 'self'; script-src 'self' example.com;")  
	// .reportOnly(true) // для тестов удобно  
				)  
			);  
		return http.build();  
	}  
}
```

## Report-To header (deprecated для поддержки старых браузеров)
#report #reporting #endpoint #header #deprecated
```http
Report-To: <json-field-value>
```
[`<json-field-value>`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Report-To#json-field-value)
- [`group`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Report-To#group) имя группы эндпоинтов
- [`max_age`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Report-To#max_age) время кэша конфигурации отправки отчетов в браузере
- [`endpoints`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Report-To#endpoints) -массив урлов эндпоинтов для отчета
пример с CSP:
```http
Report-To: { "group": "csp-endpoints",
              "max_age": 10886400,
              "endpoints": [
                { "url": "https://example.com/reports" },
                { "url": "https://backup.com/reports" }
              ] }

Content-Security-Policy: script-src https://example.com/; report-to csp-endpoints
```
## Reporting-Endpoints header (современная альтернатива Report-To)
#report #reporting #endpoint #header
пример с CSP:
```http
Reporting-Endpoints: csp-endpoint="https://example.com/csp-reports"
Content-Security-Policy: default-src 'self'; report-to csp-endpoint
```

multiple:
```http
Reporting-Endpoints: csp-endpoint="https://example.com/csp-reports",
                     permissions-endpoint="https://example.com/permissions-policy-reports"
```