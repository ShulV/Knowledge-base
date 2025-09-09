
## @Primary / @Qualifier
#qualifier #primary #annotation #context 

```java
org.springframework.context.annotation
```

Аннотация _@Primary_ задает бин, который будет внедрен по умолчанию (при отсутствии других указаний).

Аннотация _@Qualifier_ позволяет уточнить **имя бина**, который надо внедрить. Используется прямо перед аргументом.


```java
//конструктор
public AlfaBankService(@Qualifier("alfaBankRestTemplate") RestTemplate restTemplate){

this.restTemplate=restTemplate;

}
```
внедрили бин в контекст так:
```java
@Bean(value = "alfaBankRestTemplate")  
public RestTemplate alfaBankRestTemplate() {
//...
}
```

P.S. если нет @Primary на данный класс/интерфейс, и нет @Qualifier, но реализаций для внедрения несколько будет ошибка, подсказывающая что нужно юзать Qualifier
```bash
Description:

Parameter 3 of constructor in ru.xmap.api.service.identification_system.systems.impl.id_provider.alfa_id.jms.AlfaIdIdentificationSystemListener required a single bean, but 2 were found:
<------>- alfaIdIdentificationSystemImpl: defined in file [/home/shulpov.v/IdeaProjects/application/keeper-api/build/classes/java/main/ru/xmap/api/service/identification_system/systems/impl/id_provider/alfa_id/AlfaIdIdentificationSystemImpl.class]
<------>- testIdIdentificationSystemImpl: defined in file [/home/shulpov.v/IdeaProjects/application/xmap-api/build/classes/java/main/ru/xmap/api/service/identification_system/systems/impl/id_provider/alfa_id/TestIdIdentificationSystemImpl.class]

This may be due to missing parameter name information

Action:

Consider marking one of the beans as @Primary, updating the consumer to accept multiple beans, or using @Qualifier to identify the bean that should be consumed
```


**P.S. 
@Primary создает очень много проблем при неправильном использовании!!!**

---
## Интересные способы внедрения переменных из конфига
#spring-beans #value #annotation #spel
через SpEL:
```java
@Value("#{'${listOfValues}'.split(',')}") private List<String> valuesList;
```
мапа:
```java
// в конфиге valuesMap={key1: '1', key2: '2', key3: '3'}
@Value("#{${valuesMap}}") private Map<String, Integer> valuesMap;
```

---
## Быстро протестировать метод в сервисе
#postConstruct #context #spring #spring-beans  #post #constuct #pre #event #ready
Дождется, пока внедрятся бины в текущий сервис и создатся сам сервис
```java
@PostConstruct
void onConstructed() {  
    log.info("Some bean was created and dependent beans were autowired"); 
}
```

Дождется, пока загрузится весь контекст приложения
```java
@EventListener(ApplicationReadyEvent.class)  
void onApplicationReady() {  
    log.info("Context was loaded");  
}
```

Практического примера, кроме как остановка приложения, не пришло в голову. Можно сделать так:
```java
@PreDestroy  
public void onDestroyed() {  
    log.info("Application stopped");  
}
```