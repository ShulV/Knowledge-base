
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


---

## rollbackFor
#rollback #rollbackFor #transactional 
```java
@Transactional(noRollbackFor = {ServiceException.class})
```
P.S. значение ServiceException.class будет соответствовать только выброшенным исключениям типа ServiceException и его подклассам.

- Исключения, указанные в параметре `rollbackFor` или `noRollbackFor` во внешнем методе, определяют поведение отката всей транзакции.
- Исключения, перечисленные во внутренних методах, действуют только локально и не отменяют и не заменяют правила внешнего метода.
## Статус транзакции в runtime
#runtime #status #state #transactional #trans

```java
TransactionAspectSupport.currentTransactionStatus();
```
можно пометить транзакцию к откату:
```java
TransactionAspectSupport.currentTransactionStatus().setRollbackOnly()
```


---
## TransactionDefinition
#TransactionDefinition #transactional #definition
документация:
> Настройки уровня изоляции и тайм-аута не будут применены, если не будет начата новая транзакция

---

## Работа перевода исключений в Spring (Repository)
#translation #exception #repository #interceptor 
Фреймворк Spring предоставляет специальное средство перехвата исключений — **PersistenceExceptionTranslationInterceptor**. Этот аспект выполняется автоматически, если репозиторий или DAO-класс аннотирован специальным образом (обычно аннотацией `@Repository`).

Работа осуществляется примерно так:
1. Ваш код производит какую-нибудь операцию с базой данных (например, сохранение или выборка данных).
2. Если эта операция порождает какое-либо низкоуровневное исключение (например, нарушение целостности данных в JDBC или OOM-ошибку в Hibernate), фреймворк перехватывает это исключение.
3. Затем фреймворк переводит это низкое исключение в стандартизированное Spring-исключение (например, `DataIntegrityViolationException`, `BadSqlGrammarException` и т.п.).
4. Уже переведенное исключение распространяется дальше вверх по стэку вызовов.
##### Зачем нужен `throws`-список в сигнатуре метода?
Если ваш метод объявляет, что может выбрасывать определённые конкретные исключения (указывая их в секции `throws`), фреймворк перестанет переводить их автоматически. То есть, если ваше исключение явно объявлено в сигнатуры метода, оно останется в своём оригинальном виде и не будет подвергнуто переводу.
##### Простой пример:
Представим метод, работающий с базой данных:
```java
@Repository
public class UserDao {
    @Transactional
    public void saveUser(User user) throws SQLException {
        jdbcTemplate.update("INSERT INTO USERS (...) VALUES (...)", ...);
    }
}
```
Если в этом методе случится ошибка, связанная с нарушением уникальности первичного ключа (например, дубликат записи), будет выброшено исключение типа `SQLException`. Поскольку метод объявлен с типом исключения `SQLException`, фреймворк **не станет переводить** это исключение в стандартное Spring-исключение (например, `DuplicateKeyException`).

Но если убрать `throws SQLException`, фреймворк автоматически перехватит и переведёт исключение, выдав вам высокоуровневую версию (например, `DataIntegrityViolationException`).

---
# переопределение поведения транзакции
#override #transactional #modifying
см. аннотацию
```java
@Modifying
```