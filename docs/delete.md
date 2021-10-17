Delete
=============

__1. DELETE란__  

  delete는 테이블에서 데이터를 삭제할 때 사용.  

<br/>

__2. 기본사용예시__

  DELETE FROM <테이블명> WHERE <조건문>  
  
```
SELECT * FROM example.insert_test2;
DELETE FROM example.insert_test2 WHERE seq = 24;
SELECT * FROM example.insert_test2;
DELETE FROM example.insert_test2 WHERE seq > 22;
SELECT * FROM example.insert_test2;
```

<br/>

__3. 모든 데이터 삭제__

  테이블 내 모든 데이터를 삭제하려면, WHERE절을 생략하거나 1=1 이라는 조건을 입력.  
  (모든 조건을 참으로 인식하겠다는 의미)  

```
CREATE TABLE example.delete_test AS SELECT * FROM example.insert_test2 WHERE 1=1;
DELETE FROM example.delete_test;
SELECT * FROM example.delete_test;

CREATE TABLE example.delete_test2 AS SELECT * FROM example.insert_test2 WHERE 1=1;
DELETE FROM example.delete_test2 WHERE 1=1;
SELECT * FROM example.delete_test2;

DELETE FROM example.insert_test2 WHERE 1=2; //1=2라고 입력하면 참이 아니므로 아무 데이터도 삭제되지 않음.
SELECT * FROM example.insert_test2;
```

<br/>

__4. SELECT한 결과로 DELETE하기__

  한 테이블을 SELECT 해서 조건을 불러와 다른 테이블의 데이터를 삭제할 수 있다.  
  insert_test2 테이블에 있는 seq에 해당하는 데이터를 insert_test 테이블에서 삭제한다.  
  
```
DELETE FROM example.insert_test WHERE seq in (SELECT seq FROM example.insert_test2);
SELECT * FROM example.insert_test;
```

<br/>
