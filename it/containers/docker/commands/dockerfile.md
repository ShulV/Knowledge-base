
---
## Простой пример
```bash
FROM openjdk:21
COPY ./build/libs/Xmap-API-0.1-SNAPSHOT.jar /app/xmap.jar
WORKDIR /app
ENTRYPOINT ["java", "-jar", "xmap.jar"]
```
---
## Сборка
#build #docker
```bash
docker build . -t xmap-image
```
`-t` - имя образа

---
