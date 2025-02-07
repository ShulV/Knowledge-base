
## Remote JDM debug
#remote #debug #jvm #jdwp

- добавил в /etc/systemd/system конфиги для сервисов с постфиксами "-debug"
- все проверил, дебажится
- порты для дебага:
    
- запускать и останавливать через systemctl как и обычные приложения.

Когда используются debug сервисы, обычные нужно останавливать

Настройка конфига в Intellij
![[Pasted image 20250207150009.png]]

```bash
#2024-08-16 11:45

[Unit]
Description=Xmap API
After=syslog.target

[Service]
MemoryAccounting=yes
WorkingDirectory=/srv/xmap-api
User=xmap-api
Group=xmap-api
Environment="JAVA_HOME=/usr/lib/jvm/jdk-21.0.1+12-jre"
ExecStartPre=-/bin/mkdir -p /srv/xmap-api/logs
ExecStart=/usr/lib/jvm/jdk-21.0.1+12-jre/bin/java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:10700 -Xms64M -Xmx1024M -Dfile.encoding=UTF-8 -DjvmRoute=worker-xmap-api1 -Duser.language=ru -Duser.timezone=Europe/Moscow -XX:+HeapDumpOnOutOfMemoryError -XX:+CrashOnOutOfMemoryError -jar /srv/xmap--api/xmap-api.jar
SuccessExitStatus=143
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

для удаленного дебага добавлено вот это:
```
-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:10700
```

10700 - порт на котором будет происходить отладка и что-то вроде "синхронизации" JVM, проброса её состояния

---

