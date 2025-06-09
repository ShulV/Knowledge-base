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

