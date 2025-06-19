```bash
version: '3.8'

services:

  pg15:

    image: postgres:15

    environment:

      POSTGRES_PASSWORD: 'rootroot'

    ports:

      - '3333:5432'

    volumes:

      - type: bind

        source: C:\tmp\sql

        target: /docker-entrypoint-initdb.d

#  pg14:

#    image: postgres:14

#    environment:

#      POSTGRES_PASSWORD: 'rootroot'

#    ports:

#      - '2222:5432'

#    volumes:

#      - type: bind

#        source: C:\tmp\sql

#        target: /docker-entrypoint-initdb.d        

#  pg13:

#    image: postgres:13

#    environment:

#      POSTGRES_PASSWORD: 'rootroot'

#    ports:

#      - '1111:5432'

#    volumes:

#      - type: bind

#        source: C:\tmp\sql

#        target: /docker-entrypoint-initdb.d

  my-nginx:

    image: nginx

    ports:

      - '80:80'

    volumes:

      - type: bind

        source: c:\tmp\nginx

        target: /usr/share/nginx/html
```