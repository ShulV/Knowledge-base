## RateLimiter с интервальным пополнением кол-ва запросов
#rate #limit #limiter #limiting #bucket #refill  #bucket4j
```java
import io.github.bucket4j.Bandwidth;  
import io.github.bucket4j.Bucket;  
import io.github.bucket4j.Bucket4j;  
import io.github.bucket4j.Refill;  
import org.springframework.stereotype.Service;  
  
import java.time.Duration;  
import java.util.Map;  
import java.util.concurrent.ConcurrentHashMap;  

public class RequestLimitServiceImpl implements RequestLimitService {  
  
    private static final long CAPACITY = 10;  
    private static final long INCREMENT = 10;  
    private static final long DURATION = 1;  
  
    private final Map<Long, Bucket> cache = new ConcurrentHashMap<>();  
  

    @Override  
    public Bucket resolveBucket(long apiKey) {  
        return cache.computeIfAbsent(apiKey, this::newBucket);  
    }  
  
    private Bucket newBucket(Long apiKey) {  
	    // Refill: каждую минуту добавляет 10 токенов (INCREMENT=10, DURATION=1)
        Refill refill = Refill.intervally(INCREMENT, Duration.ofMinutes(DURATION));  
		
		// Bucket: готовый счетчик с лимитами
        return Bucket4j.builder()  
                .addLimit(Bandwidth.classic(CAPACITY, refill))  // Bandwidth: ведро на 10 токенов (CAPACITY=10) с указанным пополнением
                .build();  
    }  
  
}
```

P.S. **Лимит**: максимум 10 запросов в минуту на каждый `apiKey`. Минутный интервал срабатывает независимо от количества запросов.
Данное решение хранит все ключи в RAM.

Как использовать
```java
Bucket bucket = requestLimitService.resolveBucket(apiKeyId); 
if (bucket.tryConsume(1)) { 
	// OK: запрос прошел (токен потрачен) 
} else { 
	// 429 Too Many Requests 
}
```

---

