
---
## Посмотреть java процессы
#java #process

```bash
ps -ef | grep java | awk '{printf "%-8s %-8s %-8s %-20s\n", $1, $2, $3, $NF}'  
```

пример вывода:
```bash
shulpov+ 5536     2670     com.intellij.idea.Main  
shulpov+ 10043    5536     8.8                    
shulpov+ 31671    5536     ru.xmap.api.XmapAPI  
shulpov+ 86733    9548     java
```

P.S. можно по PID убить процесс

---

#kill #command #terminal  #linux 
#### Дропнуть все джава процессы
```
killall java -9
```