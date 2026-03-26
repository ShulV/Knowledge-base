## Решение проблемы с составным PK
#composite #pk #jpa #hql 
```java
public class ClientWorkspacePK implements Serializable {  
    private Client employee;  
    private Workspace workspace;  
    private Date dateAdd;
//setter and getters

//equals and hashcode
```

```java
@Entity  
@IdClass(ClientWorkspacePK.class)  
@Table(name = "client_workspace")  
public class ClientWorkspace implements Serializable {  
  
    @Id  
    @JoinColumn(name = "employee", referencedColumnName = "id")  
    @ManyToOne(fetch = FetchType.LAZY)  
    @Schema(description = "Клиент")  
    private Client employee;  
  
    @Id  
    @JoinColumn(name = "workspace", referencedColumnName = "id")  
    @ManyToOne(fetch = FetchType.LAZY)  
    @Schema(description = "Клиент")  
    private Workspace workspace;  
  
    @Id  
    @Column(name = "date_add")  
    @Schema(description = "Дата добавления")  
    private Date dateAdd;

	//...
```

P.S. дока @IdClass: имена составных частей PK должны совпадать, типы тоже

Baeldung:
- The composite primary key class must be public.
- It must have a no-arg constructor.
- It must define the equals() and hashCode() methods.
- It must be Serializable.

Так же можно через `@Embeddable` и `@EmbeddedId`, тогда поля будут выносить в PK-класс. Меньше кода, но поля вынесены.

ВАЖНО НАСТРОИТЬ ПРАВИЛЬНО, ИНАЧЕ БУДЕТ АФФЕКТИТЬ НА JPQL, HQL, CriteriaQuery

---

# Пример использования  persistence.Tuple
#tuple #persistence #object #ql #query #hql #hibernate

P.S. красивее, чем мапить в Object.
- для Tuple обязательно нужны alias'ы `c.id AS id, c.login AS login`
- нужен query language. На нативном не получится.

```java
String employeeEmail = null;  
Long employeeId = null;  
try {  
    Tuple result = entityManager.createQuery("""  
        SELECT c.id AS id, c.login AS login  
          FROM Client c  
         WHERE c.id IN (SELECT CAST(osa.value AS long)  
                          FROM OperationSystemAttribute osa  
                         WHERE osa.operation = :operationId  
                           AND osa.name = :empIdOperationSysAttrName)  
    """, Tuple.class)  
            .setParameter("operationId", instance.getId())  
            .setParameter("empIdOperationSysAttrName", Attributes.SystemAttributes.Baas.Client.EMPL_ID)  
            .setMaxResults(1)  
            .getSingleResult();  
    employeeId = ((Number) result.get("id")).longValue();  
    employeeEmail = (String) result.get("login");  
} catch (Exception ex) {  
    log.error("Cannot send compliance email, cannot get employee email from operation system attributes: " +  
                    "[person_id = '{}', operation_id = '{}']",  
            securityBean.getPerson().getId(), instance.getId(), ex);  
}
```

вариант с Object:
```java
Object[] result = (Object[]) entityManager.createNativeQuery("""  
    SELECT id, login      
      FROM client     
     WHERE id IN (SELECT CAST(value AS BIGINT)                    
			        FROM operation_system_attribute                  
			       WHERE operation = :operationId                    
			         AND name = :empIdOperationSysAttrName)     
	 LIMIT 1""")  
        .setParameter("operationId", instance.getId())  
        .setParameter("empIdOperationSysAttrName", Attributes.SystemAttributes.Baas.Client.EMPL_ID)  
        .getSingleResult();  
employeeId = ((Number) result[0]).longValue();  
employeeEmail = (String) result[1];
```