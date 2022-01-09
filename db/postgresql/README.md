## postgresql 도커 생성과 함께 db, table 셋업하기

- `/docker-entrypoint-initdb.d/` 디렉토리에 초기화에 사용할 .sql 파일을 넣어준다.
- 파일이 여러 개일 경우, 이름순으로 동작함에 주의한다.

### 예시

```
version: "3.7"

services:
  db:
    image: postgres:14.1
    container_name: db
    environment:
      - POSTGRES_USER=test
      - POSTGRES_PASSWORD=test
    ports:
      - '5432:5432'
    volumes:
      - ./db/data/:/var/lib/postgresql/data
      - ./db/init:/docker-entrypoint-initdb.d
```

docker-compose.yaml 에 다음과 같이 볼륨을 연결하고, db/init 디렉토리에 도커 생성과 함께 실행할 sql 파일을 담아준다.

- /db/init/0-schema.sql
- /db/init/1-data.sql

```
db  | 2022-01-09 13:46:34.538 UTC [49] LOG:  database system is ready to accept connections
db  |  done
db  | server started
db  | CREATE DATABASE
db  | 
db  | 
db  | /usr/local/bin/docker-entrypoint.sh: running /docker-entrypoint-initdb.d/0-schema.sql
db  | CREATE DATABASE
db  | You are now connected to database "test" as user "test_user".
db  | CREATE TABLE
db  | ALTER TABLE
db  | CREATE TABLE
db  | ALTER TABLE
db  | CREATE INDEX
db  | CREATE INDEX
db  | CREATE TABLE
db  | ALTER TABLE
db  | CREATE INDEX
db  | CREATE INDEX
db  | 
db  | 
db  | /usr/local/bin/docker-entrypoint.sh: running /docker-entrypoint-initdb.d/1-data.sql
db  | You are now connected to database "test" as user "test_user".
db  | INSERT 0 1
```

도커 생성시 로그를 확인하여 동작 여부를 알 수 있다.


### Reference
- https://hub.docker.com/_/postgres


### postgresql에서 .sql 파일에서 DB 전환은?

- 그냥 똑같이 `\c db_name` 사용한다.