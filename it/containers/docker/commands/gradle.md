
---
## manifest
#docker #manifest #gradle 
P.S. в build.gradle
```gradle
// Так в jar в /META-INF/MANIFEST.MF будет строка с указанием main-класса  
jar {  
    manifest {  
       attributes 'Main-class' : 'com.xmap_api.XmapApiApplication'  
    }  
}
```

P.S. Это нужно докеру

---
## Сборка jar для докер для spring boot
```
gradle bootJar
```
P.S. создает jar с нужными зависимостями

---

