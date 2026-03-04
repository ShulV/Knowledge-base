## Вывод stacktrace в лог
#stacktrace #trace #log
```java
log.info("Some method stacktrace: [stacktrace_10 = '{}']", Arrays.toString(Arrays.copyOfRange(Thread.currentThread().getStackTrace(), 0, 10)));
```

P.S. вывод цепочки 10 последних вызовов

---

## Logback маскирование
#mask #logback #ch #qos #encoding #wrapping #wrapper #pattern #appender #layout #masking #password
```xml
<?xml version="1.0" encoding="UTF-8"?>  
  
<configuration>  
    <property name="LOG_FOLDER" value="logs"/>  
    <property name="LOG_PATTERN" value="%d{dd-MM-yyyy HH:mm:ss.SSS} [%thread] %level %logger{36} - %msg traceId: %X{trace_id}%n"/>  
  
    <appender name="MAIN-FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">  
       <file>${LOG_FOLDER}/main.log</file>  
       <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">  
          <Pattern>             ${LOG_PATTERN}  
          </Pattern>  
       </encoder>       
       <encoder class="ch.qos.logback.core.encoder.LayoutWrappingEncoder">  
          <layout class="ru.some-path.MaskingPatternLayout">  
             <patternsProperty>(?:numberAfterPrefix|postcode|postalCode|phone|phoneNumber|number|line1|address|townOrCity|email|firstName|lastName|password|passwordHash|newPin|otp|pan|fromPan|pan2|toPan|exp|expiry|fromExpiry|cvc|cvc2|fromCvc|nameOnCard|cardToken|verificationNumber|totpCode|accessToken|refreshToken|zendeskIdentToken|challenge|fileBase64)"[: ]+"([^"]+)"|(?:authorization|sl-client-pwd-hash)=([^;]+)</patternsProperty>  
             <pattern>${LOG_PATTERN}</pattern>  
          </layout>       
       </encoder>  
       <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">  
          <fileNamePattern>             ${LOG_FOLDER}/archived/main.%d{yyyy-MM-dd}.log.gz  
          </fileNamePattern>  
       </rollingPolicy>    
    </appender>
       
       .....
```

P.S. класс маскирования унаследовать от `public class PatternLayout extends PatternLayoutBase<ILoggingEvent>` и переопределить метод doLayout