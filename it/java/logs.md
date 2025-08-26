## Вывод stacktrace в лог
#stacktrace #trace #log
```java
log.info("Some method stacktrace: [stacktrace_10 = '{}']", Arrays.toString(Arrays.copyOfRange(Thread.currentThread().getStackTrace(), 0, 10)));
```

P.S. вывод цепочки 10 последних вызовов

---
