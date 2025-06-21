##  управление сетями
```bash
docker network create <network_name> <container_name>
docker network ls
docker network connect <network_name> <container_name>
docker network prune
docker network inspect <network_name>
```

## compose
P.S. если не указываем сеть явно, докер все равно создаст bridge. Так не рекомендуется делать.
```yml
%% ... %%
services:
  pg-17:
	%% ... %%
    network:
    - network-1
  spring-app:
    %% ... %%
    network:
    - network-1
networks:
  network-1:
```

---
