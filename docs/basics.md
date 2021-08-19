SQL Basics
=================

* **SQL 명령어 종류**
  * DDL = Data Definition Language, 데이터 정의 언어
  * DML = Data Manipulation Language, 데이터 조작 언어
  * DCL = Data Control Language, 데이터 제어 언어

1. DDL

|명령어|기능|
| :------: | -------- |
| CREATE | DB 내 개체 생성 | 
| DROP | DB 내 개체 삭제 |
| ALTER | DB 내 개체의 속성 및 정의 변경 |
| RENAME | DB 내 개체 이름 변경 |
| TRUNCATE | 테이블 내 모든 데이터 빠르게 삭제 |


2. DML

|명령어|기능|
|:------:|--------|
|INSERT|특정 테이블에 데이터 신규 삽입|
|UPDATE|특정 테이블 내 데이터 전체 또는 일부를 새로운 값으로 갱신|
|DELETE|특정 테이블 내 데이터 전체 또는 일부 삭제|
|SELECT|특정 테이블 내 데이터 전체 또는 일부 선택|


3. DCL

|명령어|기능|
|:------:|--------|
|GRANT|DB 사용자에게 특정 작업의 수행권한 부여|
|REVOKE|DB 사용자에게 부여권 수행권한 박탈|
|SET TRANSACTION|트랜잭션 모드로 설정|
|BEGIN|트랜잭션의 시작|
|COMMIT|트랜잭션 실행|
|ROLLBACK|트랜잭션 취소|
|SAVEPOINT|롤백 지점 설정|
|LOCK|테이블 자원 점유|
