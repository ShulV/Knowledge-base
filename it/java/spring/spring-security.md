
## Архитектура Servlet Filters
![[Pasted image 20241228121229.png]]
[servlet-filters-review][https://docs.spring.io/spring-security/reference/servlet/architecture.html#servlet-filters-review]
[spring-security-architecture-and-internal-workflow][https://riteshpanigrahi.com/spring-security-architecture-and-internal-workflow]

## Фильтры по умолчанию

```
org.springframework.security.web.authentication.       AnonymousAuthenticationFilterorg.springframework.security.web.csrf.                 CsrfFilterorg.springframework.security.web.session.              DisableEncodeUrlFilterorg.springframework.security.web.access.               ExceptionTranslationFilterorg.springframework.security.web.header.               HeaderWriterFilterorg.springframework.security.web.authentication.logout.LogoutFilterorg.springframework.security.web.savedrequest.         RequestCacheAwareFilterorg.springframework.security.web.servletapi.           SecurityContextHolderAwareRequestFilterorg.springframework.security.web.context.              SecurityContextPersistenceFilterorg.springframework.security.web.session.              SessionManagementFilterorg.springframework.security.web.context.request.async.WebAsyncManagerIntegrationFilter
```

----
## Отключить по-дефолту настроенные фильтры
```
@EnableWebSecuritypublic class SecurityFilterChainImpl {    @Bean    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {        return http                .anonymous(AbstractHttpConfigurer::disable)         // AnonymousAuthenticationFilter                .csrf(AbstractHttpConfigurer::disable)              // CsrfFilter                .sessionManagement(AbstractHttpConfigurer::disable) // DisableEncodeUrlFilter, SessionManagementFilter                .exceptionHandling(AbstractHttpConfigurer::disable) // ExceptionTranslationFilter                .headers(AbstractHttpConfigurer::disable)           // HeaderWriterFilter                .logout(AbstractHttpConfigurer::disable)            // LogoutFilter                .requestCache(AbstractHttpConfigurer::disable)      // RequestCacheAwareFilter                .servletApi(AbstractHttpConfigurer::disable)        // SecurityContextHolderAwareRequestFilter                .securityContext(AbstractHttpConfigurer::disable)   // SecurityContextPersistenceFilter                .build();    }}
```

----
## Фильтры переопределенные спрингом и их порядковые номера
|                                                                     |                                          |                  |
| ------------------------------------------------------------------- | ---------------------------------------- | ---------------- |
| пакет                                                               | класс                                    | порядковый номер |
| org.springframework.security.web.session.                           | DisableEncodeUrlFilter                   | 100              |
| org.springframework.security.web.session.                           | ForceEagerSessionCreationFilter          | 200              |
| org.springframework.security.web.access.channel.                    | ChannelProcessingFilter                  | 300              |
| org.springframework.security.web.context.request.async.             | WebAsyncManagerIntegrationFilter         | 500              |
| org.springframework.security.web.context.                           | SecurityContextHolderFilter              | 600              |
| org.springframework.security.web.context.                           | SecurityContextPersistenceFilter         | 700              |
| org.springframework.security.web.header.                            | HeaderWriterFilter                       | 800              |
| org.springframework.web.filter.                                     | CorsFilter                               | 900              |
| org.springframework.security.web.csrf.                              | CsrfFilter                               | 1000             |
| org.springframework.security.web.authentication.logout.             | LogoutFilter                             | 1100             |
| org.springframework.security.oauth2.client.web.                     | OAuth2AuthorizationRequestRedirectFilter | 1200             |
| org.springframework.security.saml2.provider.service.servlet.filter. | Saml2WebSsoAuthenticationRequestFilter   | 1300             |
| org.springframework.security.web.authentication.preauth.x509.       | X509AuthenticationFilter                 | 1400             |
| org.springframework.security.web.authentication.preauth.            | AbstractPreAuthenticatedProcessingFilter | 1500             |
| org.springframework.security.cas.web.                               | CasAuthenticationFilter                  | 1600             |
| org.springframework.security.oauth2.client.web.                     | OAuth2LoginAuthenticationFilter          | 1700             |
| org.springframework.security.saml2.provider.service.servlet.filter. | Saml2WebSsoAuthenticationFilter          | 1800             |
| org.springframework.security.web.authentication.                    | UsernamePasswordAuthenticationFilter     | 1900             |
| org.springframework.security.openid.                                | OpenIDAuthenticationFilter               | 2100             |
| org.springframework.security.web.authentication.ui.                 | DefaultLoginPageGeneratingFilter         | 2200             |
| org.springframework.security.web.authentication.ui.                 | DefaultLogoutPageGeneratingFilter        | 2300             |
| org.springframework.security.web.session.                           | ConcurrentSessionFilter                  | 2400             |
| org.springframework.security.web.authentication.www.                | DigestAuthenticationFilter               | 2500             |
| org.springframework.security.oauth2.server.resource.web.            | BearerTokenAuthenticationFilter          | 2600             |
| org.springframework.security.web.authentication.www.                | BasicAuthenticationFilter                | 2700             |
| org.springframework.security.web.savedrequest.                      | RequestCacheAwareFilter                  | 2800             |
| org.springframework.security.web.servletapi.                        | SecurityContextHolderAwareRequestFilter  | 2900             |
| org.springframework.security.web.jaasapi.                           | JaasApiIntegrationFilter                 | 3000             |
| org.springframework.security.web.authentication.rememberme.         | RememberMeAuthenticationFilter           | 3100             |
| org.springframework.security.web.authentication.                    | AnonymousAuthenticationFilter            | 3200             |
| org.springframework.security.oauth2.client.web.                     | OAuth2AuthorizationCodeGrantFilter       | 3300             |
| org.springframework.security.web.session.                           | SessionManagementFilter                  | 3400             |
| org.springframework.security.web.access.                            | ExceptionTranslationFilter               | 3500             |
| org.springframework.security.web.access.intercept.                  | FilterSecurityInterceptor                | 3600             |
| org.springframework.security.web.access.intercept.                  | AuthorizationFilter                      | 3700             |
| org.springframework.security.web.authentication.switchuser.         | SwitchUserFilter                         | 3800             |
|                                                                     |                                          |                  |


----
## DelegatingFilterProxy и цепочка аутентификации

1) DelegatingFilterProxy вызывает FilterChainProxy
2) FilterChainProxy вызывает SecurityFilterChain
3) SecurityFilterChain - цепочка фильтров spring security

FilterChainProxy:
- регистрирует фильтры securty (бины)
- очищает SecurityContext, чтобы избежать утечек памяти
- применяет HttpFirewall Spring Security для защиты приложений от определенных типов атак. [httpFirewall](https://docs.spring.io/spring-security/reference/servlet/exploits/firewall.html#servlet-httpfirewall)

DelegatingFilterProxy:
- делегирует аутентификацию Authentication Manager'у
	- Authentication Manager делегирует аутентификацию ProviderManager'у
		- Provider Manager проходит по всем Auth Provider'ам, вызывает у них метод supports(auth), который проверяет подходит 
		- Provider Manager сравнивает UserDetails с теми credentials, что прислали в запросе. Отдает authentication object фильтрам, если всё ок, а они сохраняют его в Security Context

UserDetailsService:
- предоставляет сведения о пользователе из системы
- получает UserDetails из БД или другого места для проверки credentials