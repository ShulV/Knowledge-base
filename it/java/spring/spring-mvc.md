
---

## Разница между Filter и Interceptor
#filter #interceptor #mvc #dispatcher #servlet #context #фильтр #интерцептор

### Фильтры
 javax.servlet.Filter
```java
@Component public class LogFilter implements Filter { 
	private Logger logger = LoggerFactory.getLogger(LogFilter.class); 
	@Override 
	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
		logger.info("Hello from: " + request.getLocalAddr());
		chain.doFilter(request, response); 
	} 
}
```

Задачи:
- Выполнение до dispatcherServlet
- Выполнение до контроллера
- Аутентификация
- Ведение журнала и аудит
- Сжатие изображений и данных
- Любая функциональность, которую мы хотим отделить от Spring MVC.

### Интерцепторы

org.springframework.web.servlet.HandlerInterceptor
```java
public class LogInterceptor implements HandlerInterceptor {
	private Logger logger = LoggerFactory.getLogger(LogInterceptor.class);
	@Override
	public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
		logger.info("preHandle"); 
		return true; 
	}
	
	@Override
	public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
		logger.info("postHandle"); 
	}
	
	@Override
	public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
		logger.info("afterCompletion"); 
	} 
}
```

Задачи:
- Выполнение после dispatcherServlet
- Выполнение до контроллера
- Решение сквозных проблем, таких как ведение журнала приложений. 
- Подробные проверки авторизации 
- Манипулирование контекстом или моделью Spring
- Предоставление доступа к объектам Handler и ModelAndView

---

##