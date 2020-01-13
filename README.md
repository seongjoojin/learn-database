# learn-database

생활코딩에서 데이터베이스에 대해서 배운 내용을 정리하는 레포입니다.

## DATABASE1

- database : 데이터를 저장하고 출력하기 위한 전문적인 소프트웨어
- database 제품군 : MySQL, Oracle, SQL Server, PostgreSQL, Mongo DB 등등

### 데이터베이스의 본질

- input: Create, Update, Delete
- output: Read

### file vs database

- text file => spreadsheet(excel)
- Database는 컴퓨터 언어를 통해서 자동화할 수 있음.

### 수업을 마치며

- 회사에서 이미 정해놓은 데이터베이스가 있다면 그것을 사용해야함
- https://db-engines.com/en/ranking
- 데이터베이스 시장의 절대 강자는 관계형 데이터베이스
- 관계형 데이터베이스 중에 하나를 골라서 공부하고 그 다음에 관계형 데이터베이스가 아닌 것을 공부하는 것을 추천
- 관계형 데이터베이스는 1970년대부터 개발되어 데이터베이스의 강자로 존재하였음.
- IoT, SNS 등이 등장하면서 기존의 관계형 데이터베이스의 한계가 나타나게 되고 2010년에 관계형 데이터베이스가 아닌 것들이 등장하게 됨 (NoSQL)
- Oracle : 오래동안 절대 강자를 지킨 데이터베이스. 관공서, 큰 기업 (비용이 비싸고 기술지원도 비쌈), 금융 (신뢰성이 필요한 곳에서 주로 사용)
- MySQL : 무료고 오픈소스임. 개인 ,작은 기업, SNS에서 사용하기 적합 => 초심자에게 추천

## DATABASE2 - MySQL

- 1994년 스웨덴에서 개발되기 시작한 MySQL.
- 무료이고 오픈소스.
- MySQL은 WEB과 함께 폭발적으로 성장함

### 데이터베이스의 목적

- 관계형 데이터베이스는 스프레이드시트처럼 데이터를 표형태로 표현해줌
- 데이터베이스는 컴퓨터 언어를 통해서 제어할 수 있음

### MySQL 설치

각자의 운영체제에서 설치하기

- https://dev.mysql.com/downloads/mysql/

docker 이용하기

- https://hub.docker.com/_/mysql/
- https://hub.docker.com/_/mysql?tab=tags

```bash
# docekr mysql 5.7.28 이미지 설치
$ docker pull mysql:5.7.28

# mysql 이미지 실행
$ docker run -d -p 3306:3306 \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
  --name mysql \
  mysql:5.7.28
# 위의 예제는 비밀번호 없이 접속할 수 있도록 해준 것이고 비밀번호를 지정하고 싶으시면 MYSQL_ROOT_PASSWORD 의 옵션에 넣어주시면 됩니다.

# docker 컨테이너 아이디 확인
$ docker ps

# docker 컨테이너 접속
$ docker exec -it [컨테이너 아이디] /bin/bash

# 접속 후 mysql 접속
$ mysql
```

### MySQL의 구조

- 표(table) : 데이터를 기록하는 최종적인 곳
- 데이터베이스(database) : 표들을 그룹핑 한 것, 스키마(Schema) : 서로 연관된 데이터들를 그룹핑 해줌
- 데이터베이스 서버(database server)

### MySQL 서버 접속

- 데이터베이스는 파일에 비해 보안적인 면을 더 가지고 있음
- 권한 기능을 가지고 있음
- root는 모든 권한을 가지고 있음
- 권장사항으로는 root가 아닌 제한적인 유저로 접속하는 것

```bash
# root로 접속(비밀번호 입력)
$ mysql -uroot -p
```
