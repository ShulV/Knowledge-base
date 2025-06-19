---

---

---
## Gradle/java compatibility
#compatibility #совместимость #matrix #version #java #gradle

| Java version | Support for toolchains | Support for running Gradle |     |
| ------------ | ---------------------- | -------------------------- | --- |
| 8            | N/A                    | 2.0                        |     |
| 9            | N/A                    | 4.3                        |     |
| 10           | N/A                    | 4.7                        |     |
| 11           | N/A                    | 5.0                        |     |
| 12           | N/A                    | 5.4                        |     |
| 13           | N/A                    | 6.0                        |     |
| 14           | N/A                    | 6.3                        |     |
| 15           | 6.7                    | 6.7                        |     |
| 16           | 7.0                    | 7.0                        |     |
| 17           | 7.3                    | 7.3                        |     |
| 18           | 7.5                    | 7.5                        |     |
| 19           | 7.6                    | 7.6                        |     |
| 20           | 8.1                    | 8.3                        |     |
| 21           | 8.4                    | 8.5                        |     |
| 22           | 8.7                    | 8.8                        |     |
| 23           | N/A                    | N/A                        |     |
|              |                        |                            |     |
[Таблица в инете](https://docs.gradle.org/current/userguide/compatibility.html)
Совместимость spring boot и java: [[spring-boot#Java Compatibility]]

---
## MANIFEST
#manifest
P.S. в build.gradle
```gradle
// Так в jar в /META-INF/MANIFEST.MF будет строка с указанием main-класса  
jar {  
    manifest {  
       attributes 'Main-class' : 'com.xmap_api.XmapApiApplication'  
    }  
}
```

P.S. Это нужно, например, докеру

---
## jar VS plain jar
#plain #jar #gradle 
#### Основные отличия:
- **Стандартность**: `jar` является стандартной задачей Gradle, автоматически включающей классы и ресурсы проекта, тогда как `plainJar` создается специально для специфичных нужд.
- **Контент**: `jar` упаковывает весь проект, включая зависимости, если настроено; `plainJar` же позволяет точно контролировать содержимое файла.
- **Назначение**: `jar` чаще всего используется для развертывания приложений и библиотек, а `plainJar` — для специальных случаев вроде передачи ограниченного набора классов/ресурсов.
---
