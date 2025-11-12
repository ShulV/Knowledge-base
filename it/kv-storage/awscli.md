## Настройка подключения

>Перед тем как выполнять команды, нужно настроить AWS CLI, чтобы он знал, куда подключаться
##### 🔧 Настройка профиля для MinIO:

```
aws configure --profile minio
```

Когда CLI спросит, введи свои данные:
```
AWS Access Key ID [None]: minioadmin
AWS Secret Access Key [None]: minioadmin123
Default region name [None]: us-east-1
Default output format [None]: json
```

## Проверка соединения
```
aws --endpoint-url http://172.17.0.2:9000 s3 ls
```
если выдает ошибку - не законнектились

## Работа с бакетами
#backet
создание бакета
```
aws --endpoint-url http://localhost:9000 s3 mb s3://test-bucket
make_bucket: test-bucket
```
команда выводит доступные бакеты
```
aws --endpoint-url http://localhost:9000 s3 ls
2025-11-12 15:40:35 test-bucket
```
создать и загрузить файл:
```
echo "Привет, MinIO!" > hello.txt
aws --endpoint-url http://localhost:9000 s3 cp hello.txt s3://test-bucket/
aws --endpoint-url http://localhost:9000 s3 cp hello.txt s3://test-bucket/5b932ff4-fac9-4523-b47a-29909460b636
upload: ./hello.txt to s3://test-bucket/hello.txt 
```
> P.S. если сами не указали ID, взялось название файла

посмотреть содержимое бакета
```
shulpov.v@fedora:~/Загрузки$ aws --endpoint-url http://localhost:9000 s3 ls s3://test-bucket
2025-11-12 15:49:43         21 5b932ff4-fac9-4523-b47a-29909460b636
2025-11-12 15:47:11         21 hello.txt
```

скачать по http просто так не получится, нужно подписать запрос (нужны доп. заголовки для авторизации)
```
shulpov.v@fedora:~/Загрузки$ curl -X GET http://localhost:9000/test-bucket/5b932ff4-fac9-4523-b47a-29909460b636
<?xml version="1.0" encoding="UTF-8"?>
<Error><Code>AccessDenied</Code><Message>Access Denied.</Message><Key>hello.txt</Key><BucketName>test-bucket</BucketName><Resource>/test-bucket/hello.txt</Resource><RequestId>187736586BA0E7B7</RequestId><HostId>dd9025bab4ad464b049177c95eb6ebf374d3b3fd1af9251148b658df7ac2e3e8</HostId></Error>
```

> P.S. MinIO требует **подписанный запрос** (по стандарту AWS Signature Version 4).
> НО! вроде либы уже умеют подписывать сообщения, зная access_key и secret_key

