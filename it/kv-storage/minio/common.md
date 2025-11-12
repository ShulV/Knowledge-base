#minio #s3 #kv #key-value #storage #aws
простой запуск
```bash
shulpov.v@fedora:~$ docker run -d \
  --name minio \
  -p 9000:9000 \
  -p 9001:9001 \
  -e MINIO_ROOT_USER=minioadmin \
  -e MINIO_ROOT_PASSWORD=minioadmin123 \
  quay.io/minio/minio server /data --console-address ":9001"
```

Далее
```
docker stop minio
docker start minio
```

P.S.

|Назначение|В контейнере|На хосте|Адрес доступа|
|---|---|---|---|
|API (S3)|`9000`|`9000`|[http://localhost:9000](http://localhost:9000/)|
|Web Console|`9001`|`9001`|[http://localhost:9001](http://localhost:9001/)|

> quay.io/minio/minio - образ

---

