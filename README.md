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

### MySQL 스키마(schema)의 사용

"mysql create database"로 검색

https://dev.mysql.com/doc/refman/5.7/en/creating-database.html

```bash
# 데이터베이스 생성
$ CREATE DATABASE [데이터베이스 이름];
```

"mysql delete database"로 검색

https://dev.mysql.com/doc/refman/5.7/en/drop-database.html

```bash
# 데이터베이스 삭제
$ DROP DATABASE [데이터베이스 이름];
```

- 명령어를 외우는게 아니라 검색하는 방법이 나음
- 예) 데이터베이스 내용을 보고 싶을 때 "how to show database in mysql"로 검색

https://dev.mysql.com/doc/refman/5.7/en/show-databases.html

```bash
# 데이터베이스 조회
$ SHOW DATABASES;

# 데이터베이스 사용
$ USE [데이터베이스 이름];
```

### SQL과 테이블의 구조

- SQL(Structured Query Language) : 쉽고 중요함.(수많은 관계형 데이터베이스들의 표준화된 언어)
- table(표) : 행(row,record)와 열(column)으로 이루어져 있음.

### MySQL 테이블의 생성

https://devhints.io/mysql

여러 언어에는 cheatsheet가 존재함.

https://www.techonthenet.com/mysql/datatypes.php

```sql
$ CREATE TABLE topic (
  id INT(11) NOT NULL AUTO_INCREMENT,
  title VARCHAR(100) NOT NULL,
  description TEXT,
  created DATETIME NOT NULL,
  author VARCHAR(30),
  profile VARCHAR(100),
  PRIMARY KEY(id)
);
```

- AUTO_INCREMENT: 값이 1씩 자동으로 증가
- NOT NULL : 값이 없는것을 허용하지 않음
- NULL : 값이 없는 것을 허용함

- PRIMARY KEY => 성능, 중복 방지

### MySQL의 CRUD

- Create
- Read
- Update
- Delete

가장 핵심적인 기능은 Create, Read

### SQL의 INSERT 구문

테이블 구조 보기

```sql
$ DESC topic;
```

row 생성

```sql
$ INSERT INTO topic (title,description,created,author, profile) VALUES('MySQL','MySQL is ...',NOW(),'egoing','developer');
```

topic table에서 모든 데이터 조회

```sql
$ SELECT * FROM topic;
```

### SQL의 SELECT 구문

topic table에서 모든 행 조회

```sql
$ SELECT * FROM topic;

+----+------------+------------------+---------------------+--------+--------------------------+
| id | title      | description      | created             | author | profile                  |
+----+------------+------------------+---------------------+--------+--------------------------+
|  1 | MySQL      | MySQL is ...     | 2020-01-17 13:06:24 | egoing | developer                |
|  2 | ORACLE     | OCRACLE is...    | 2020-01-17 13:11:21 | egoing | developer                |
|  3 | SQL Server | SQL Server is... | 2020-01-17 13:12:42 | duru   | database administrator   |
|  4 | PostgreSQL | PostgreSQL is... | 2020-01-17 13:14:03 | taeho  | data scientist,developer |
|  5 | MongoDB    | MongoDB is...    | 2020-01-17 13:14:42 | egoing | developer                |
+----+------------+------------------+---------------------+--------+--------------------------+
```

topic table에서 id,title,created,author행 조회

```sql
$ SELECT id,title,created,author FROM topic;

+----+------------+---------------------+--------+
| id | title      | created             | author |
+----+------------+---------------------+--------+
|  1 | MySQL      | 2020-01-17 13:06:24 | egoing |
|  2 | ORACLE     | 2020-01-17 13:11:21 | egoing |
|  3 | SQL Server | 2020-01-17 13:12:42 | duru   |
|  4 | PostgreSQL | 2020-01-17 13:14:03 | taeho  |
|  5 | MongoDB    | 2020-01-17 13:14:42 | egoing |
+----+------------+---------------------+--------+
```

https://dev.mysql.com/doc/refman/5.7/en/select.html

topic table에서 id,title,created,author행에서 author가 egoing인 행을 조회

```sql
$ SELECT id,title,created,author FROM topic WHERE author='egoing';

+----+---------+---------------------+--------+
| id | title   | created             | author |
+----+---------+---------------------+--------+
|  1 | MySQL   | 2020-01-17 13:06:24 | egoing |
|  2 | ORACLE  | 2020-01-17 13:11:21 | egoing |
|  5 | MongoDB | 2020-01-17 13:14:42 | egoing |
+----+---------+---------------------+--------+
```

topic table에서 id,title,created,author행에서 author가 egoing인 행을 조회하고 id를 DESC로 정렬해서 조회

```sql
$ SELECT id,title,created,author FROM topic WHERE author='egoing' ORDER BY id DESC;

+----+---------+---------------------+--------+
| id | title   | created             | author |
+----+---------+---------------------+--------+
|  5 | MongoDB | 2020-01-17 13:14:42 | egoing |
|  2 | ORACLE  | 2020-01-17 13:11:21 | egoing |
|  1 | MySQL   | 2020-01-17 13:06:24 | egoing |
+----+---------+---------------------+--------+
```

topic table에서 id,title,created,author행에서 author가 egoing인 행을 조회하고 id를 DESC로 정렬하고 결과를 2개로 제한함

```sql
$ SELECT id,title,created,author FROM topic WHERE author='egoing' ORDER BY id DESC LIMIT 2;

+----+---------+---------------------+--------+
| id | title   | created             | author |
+----+---------+---------------------+--------+
|  5 | MongoDB | 2020-01-17 13:14:42 | egoing |
|  2 | ORACLE  | 2020-01-17 13:11:21 | egoing |
+----+---------+---------------------+--------+
```

### SQL의 UPDATE 구문

https://dev.mysql.com/doc/refman/5.7/en/update.html

```sql
$ DESC topic;

+-------------+--------------+------+-----+---------+----------------+
| Field       | Type         | Null | Key | Default | Extra          |
+-------------+--------------+------+-----+---------+----------------+
| id          | int(11)      | NO   | PRI | NULL    | auto_increment |
| title       | varchar(100) | NO   |     | NULL    |                |
| description | text         | YES  |     | NULL    |                |
| created     | datetime     | NO   |     | NULL    |                |
| author      | varchar(30)  | YES  |     | NULL    |                |
| profile     | varchar(100) | YES  |     | NULL    |                |
+-------------+--------------+------+-----+---------+----------------+
```

```sql
$ SELECT * FROM topic;

+----+------------+------------------+---------------------+--------+--------------------------+
| id | title      | description      | created             | author | profile                  |
+----+------------+------------------+---------------------+--------+--------------------------+
|  1 | MySQL      | MySQL is ...     | 2020-01-17 13:06:24 | egoing | developer                |
|  2 | ORACLE     | OCRACLE is...    | 2020-01-17 13:11:21 | egoing | developer                |
|  3 | SQL Server | SQL Server is... | 2020-01-17 13:12:42 | duru   | database administrator   |
|  4 | PostgreSQL | PostgreSQL is... | 2020-01-17 13:14:03 | taeho  | data scientist,developer |
|  5 | MongoDB    | MongoDB is...    | 2020-01-17 13:14:42 | egoing | developer                |
+----+------------+------------------+---------------------+--------+--------------------------+
```

```sql
$ UPDATE topic SET description='Oracle is...', title='Oracle' WHERE id=2;

$ SELECT * FROM topic;

+----+------------+------------------+---------------------+--------+--------------------------+
| id | title      | description      | created             | author | profile                  |
+----+------------+------------------+---------------------+--------+--------------------------+
|  1 | MySQL      | MySQL is ...     | 2020-01-17 13:06:24 | egoing | developer                |
|  2 | Oracle     | Oracle is...     | 2020-01-17 13:11:21 | egoing | developer                |
|  3 | SQL Server | SQL Server is... | 2020-01-17 13:12:42 | duru   | database administrator   |
|  4 | PostgreSQL | PostgreSQL is... | 2020-01-17 13:14:03 | taeho  | data scientist,developer |
|  5 | MongoDB    | MongoDB is...    | 2020-01-17 13:14:42 | egoing | developer                |
+----+------------+------------------+---------------------+--------+--------------------------+
```

UPDATE를 사용할 때 WHERE를 꼭 같이 사용해야함

### SQL의 DELETE 구문

https://dev.mysql.com/doc/refman/5.7/en/delete.html

DELETE를 사용할 때 WHERE를 꼭 같이 사용해야함

```sql
$ SELECT * FROM topic;

+----+------------+------------------+---------------------+--------+--------------------------+
| id | title      | description      | created             | author | profile                  |
+----+------------+------------------+---------------------+--------+--------------------------+
|  1 | MySQL      | MySQL is ...     | 2020-01-17 13:06:24 | egoing | developer                |
|  2 | Oracle     | Oracle is...     | 2020-01-17 13:11:21 | egoing | developer                |
|  3 | SQL Server | SQL Server is... | 2020-01-17 13:12:42 | duru   | database administrator   |
|  4 | PostgreSQL | PostgreSQL is... | 2020-01-17 13:14:03 | taeho  | data scientist,developer |
|  5 | MongoDB    | MongoDB is...    | 2020-01-17 13:14:42 | egoing | developer                |
+----+------------+------------------+---------------------+--------+--------------------------+
```

```sql
$ DELETE FROM topic WHERE id=5;

$ SELECT * FROM topic;

+----+------------+------------------+---------------------+--------+--------------------------+
| id | title      | description      | created             | author | profile                  |
+----+------------+------------------+---------------------+--------+--------------------------+
|  1 | MySQL      | MySQL is ...     | 2020-01-17 13:06:24 | egoing | developer                |
|  2 | Oracle     | Oracle is...     | 2020-01-17 13:11:21 | egoing | developer                |
|  3 | SQL Server | SQL Server is... | 2020-01-17 13:12:42 | duru   | database administrator   |
|  4 | PostgreSQL | PostgreSQL is... | 2020-01-17 13:14:03 | taeho  | data scientist,developer |
+----+------------+------------------+---------------------+--------+--------------------------+
```

### 수업의 정상

- 본질과 혁신을 분리
- Database(본질), Relational(혁신)
