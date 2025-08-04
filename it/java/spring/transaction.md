
----

## Checked и unchecked исключения в транзакциях
#rollback #rollbackFor #checked #unchecked #commit #transactional
По умолчанию Spring откатывает транзакции только в случае **непроверяемого** исключения. (unchecked: наследники Error и RuntimeException включительно).
**Проверяемые** (checked: Throwable, Exception и наследники IOException) же считаются «восстанавливаемыми» из-за чего Spring вместо `rollback` делает `commit`. (но если их указать в rollbackFor=, должны откатиться)

Чтобы откатить транзакцию, нужно заменить проверяемое исключение (например, `Exception`) на непроверяемое исключение (например, `NullPointerException`). Либо можно переопределить атрибут `rollbackFor` у аннотации.



P.S. в Kotlin нет checked/unchecked, но транзакции работают аналогично JAVA!!!


P.S. при дебаге транзакций ловить  
```java
try {
	someMethod();
} catch (Exception e) {
	//Прилетело Runtime..., а отловили как Exception...
	//Отловили как checked, прилетело unchecked
	throw e;
}
```
надо так:
```java
try {
	someMethod();
} catch (RuntimeException e) {
	//Прилетело Runtime..., а отловили как Runtime...
	//Отловили как checked, прилетело checked
	throw e;
}
```

---

## Модификаторы доступа

> Methods annotated with `@Transactional` must be overridable

P.S. метод, помеченный аннотацией `@Transcational` должен быть как минимум protected, чтобы Spring его смог переопределить для прокси-класс

P.S. аналогично метод не может быть` final`

---

## marked as rollback-only

> org.springframework.transaction.UnexpectedRollbackException: Transaction rolled back because it has been marked as rollback-only



---

## Указать дефолтное поведение rollback

```java
//As of 6.2, you can globally change the default rollback behavior – for example, through 
@EnableTransactionManagement(rollbackOn=ALL_EXCEPTIONS)
```