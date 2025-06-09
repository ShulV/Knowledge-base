## Наследование аннотаций, @Inherited
#extend #annotation #inherit

если у `@interface` есть аннотация `@Inherited`, то аннотация будет применяться при наследовании класса.

#### Пример наследуемых аннотаций:
```java
//-------------------- OPEN API (сваггер) ----------------------------
import io.swagger.v3.oas.annotations.*
@Operation
@Schema
@Content
@ApiResponse
@Parameter

//------------------------ SPRING SECURITY --------------------------
import org.springframework.security.*
@PreAuthorize
...

```

#### Пример НЕ наследуемых аннотаций
```java
//-------------------- ВАЛИДАЦИЯ -----------------------------------
import jakarta.validation.constraints.*
@Pattern
@Size
@Min
...

//-------------------- JACKSON -----------------------------------
import com.fasterxml.jackson.annotation.*
@JsonInclude
...

//-------------------- JPA -----------------------------------
import javax.persistence.*
@Table
@Column
@JoinColumn
@Entity
@Temporal
...

//--------------------- Бины ---------------------------------
import org.springframework.stereotype
@Component
@Service
@Repository
...

```

---

