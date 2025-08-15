
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

## jakarta vs spring Transaction
#jakarta #spring #transactional #ejb #javax
#### Spring `@Transactional`

The [`org.springframework.transaction.annotation.Transactional`](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/annotation/Transactional.html) annotation has been available since the 1.2 version of the Spring framework (circa 2005), and it allows you to set the following transactional properties:

- `isolation`: the underlying database isolation level
- `noRollbackFor` and `noRollbackForClassName`: the list of Java `Exception` classes that can be triggered without triggering a transaction rollback
- `rollbackFor` and `rollbackForClassName`: the list of Java `Exception` classes that trigger a transaction rollback when being thrown
- `propagation`: the transaction propagation type given by the [`Propagation`](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/annotation/Propagation.html) Enum. For instance, if the transaction context can be inherited (e.g., `REQUIRED`) or a new transaction context should be created (e.g., `REQUIRES_NEW`) or if an exception should be thrown if no transaction context is present (e.g., `MANDATORY`) or if an exception should be thrown if a current transaction context is found (e.g., `NOT_SUPPORTED`).
- `readOnly`: whether the current transaction should only read data without applying any changes.
- `timeout`: how many seconds should the transaction context be allowed to run until a timeout exception is thrown.
- `value` or `transactionManager`: the name of the Spring `TransactionManager` bean to be used when binding the transaction context.
#### Java EE `@Transactional`

The [`javax.transaction.Transactional`](https://docs.oracle.com/javaee/7/api/javax/transaction/Transactional.html) annotation was added by the Java EE 7 specification (circa 2013). So, the Java EE annotation was added 8 years later than its Spring counterpart.

The Java EE `@Transactional` defines just 3 attributes:

- `dontRollbackOn`: the list of Java `Exception` classes that can be triggered without triggering a transaction rollback
- `rollbackOn`: the list of Java `Exception` classes that trigger a transaction rollback when being thrown
- `value`: the propagation strategy, given by the [`TxType`](https://docs.oracle.com/javaee/7/api/javax/transaction/Transactional.TxType.html) Enum. For instance, if the transaction context can be inherited (e.g., `REQUIRED`) or a new transaction context should be created (e.g., `REQUIRES_NEW`) or if an exception should be thrown if no transaction context is present (e.g., `MANDATORY`) or if an exception should be thrown if a current transaction context is found (e.g., `NOT_SUPPORTED`).
