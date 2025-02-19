
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

P.S. если нет @Primary на данный класс/интерфейс, то можно писать без @Qualifier:
спринг поймет по названию какой бин внедрить (видимо, юзает рефлексию)
```java
//конструктор
public AlfaBankService(RestTemplate alfaBankRestTemplate){

this.restTemplate=alfaBankRestTemplate;

}
```


**P.S. 
@Primary создает очень много проблем при неправильном использовании!!!**

---

##