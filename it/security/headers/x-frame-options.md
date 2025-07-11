Заголовок ответа HTTP X-Frame-Options может использоваться для указания того, следует ли разрешить браузеру отображать страницу в формате <frame>, `<iframe>`, `<embed>` или `<object>`. Сайты могут использовать это, чтобы избежать атак с кликджекингом, гарантируя, что их контент не встраивается в другие сайты.

## настройка в spring boot
```java
public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {  
    return http
			//...
            .headers(header -> header  
                    .frameOptions(HeadersConfigurer.FrameOptionsConfig::sameOrigin)    
            )
```