Data dictionary
=============

__1. Data dictionary란__  

  MySQL Server 내에 있는 데이터베이스 개체에 관한 정보가 모두 모아져있는 사전.  
  DB에 어떤 user 가 있고, 어떤 스키마(데이터베이스), 테이블, 테이블 내 어떤 칼럼이 있고 데이터가 얼마나 있는지, 오브젝트가 어떤 스키마에 종속되어 있는지 등 유저가 입력하는 데이터를 제외한 모든 정보를 포함.  
  MySQL에는 information_schema, mysql, sys, performance_schema 4가지가 있으나, information_schema와 mysql 을 자주 씀.  
    
<br/>

__2. information_schema__

```
SELECT * FROM information_schema.SCHEMATA; //MySQL 내부 스키마 목록 조회

SELECT * FROM information_schema.TABLES; //MySQL 내부 테이블 정보 조회
SELECT TABLE_SCHEMA, TABLE_NAME FROM information_schema.TABLES
WHERE TABLE_SCHEMA = 'information_schema';

SELECT * FROM information_schema.COLUMNS; //MySQL 내부 칼럼 정보 조회
SELECT * FROM information_schema.COLUMNS
WHERE TABLE_SCHEMA = 'example';

SELECT * FROM information_schema.ROUTINES; //MySQL 내부 function, procedule 정보 조회
SELECT * FROM information_schema.KEY_COLUMN_USAGE; //MySQL 내부 테이블별 PK칼럼 조회
SELECT * FROM information_schema.PROCESSLIST; //MySQL에 접속중인 세션 정보 조회
```

<br/>

__3. mysql__

```
SELECT * FROM mysql.USER; //MySQL 내부 user 정보 조회
SELECT * FROM mysql.general_log; //MySQL에서 DB로그를 table로 저장하는 경우 로그 조회
SELECT * FROM mysql.slow_log; //MySQL sql 중 오래 걸리는 sql 조회(for 성능분석)
```

<br/>
