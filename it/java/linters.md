
---
## Подавление варнингов аннотацией
#warnings

```java
@SuppressWarnings("null")  
public boolean hasChild(final long parentId) {  
    return jdbcTemplate.queryForObject(  
            "        SELECT CASE WHEN exists (SELECT * FROM operation_child WHERE parent = ?) " +  
                    "            THEN 1 " +  
                    "            ELSE 0 END",  
            Long.class, parentId) == 1L;  
}
```
Параметры для аннотации (типы варнингов):
https://stackoverflow.com/questions/1205995/what-is-the-list-of-valid-suppresswarnings-warning-names-in-java