Update
=============

__1. UPDATE란__  

  insert는 테이블에 새로운 데이터를 추가해 row 수를 증가시킨다면, update는 기존 데이터의 row 수 변화없이 특정 칼럼내 값만을 바꾸는 것.  
  즉, 값을 변경하는 명령어.  
  
<br/>

__2. 사용 예시__

  UPDATE <테이블명> SET <칼럼명> = '바꿀값' WHERE <키명> = 키값  
  WHERE절에 primary key 값이 들어있는 칼럼과 키값을 써주어 해당 row 의 값을 변경하도록 함.  
  WHERE절을 쓰지 않으면 모든 row 에 대해 값이 바뀌므로 주의해야 한다.  
  단, safe update mode 로 설정이 되어있으면 에러가 뜨고 실행되지 않음.(preference > SQL editor에서 변경가능)  
  여러 줄의 row 에 대해 update 하고 싶은 경우 WHERE절에 in 조건 사용하면 됨.  
  여러 칼럼값을 변경하고 싶을 때는 SET 이후에 콤마로 구분해서 나열하면 됨.  
  
  
```
UPDATE example.insert_test SET name = '손흥민' WHERE seq = 23;
SELECT * FROM example.insert_test;
UPDATE example.insert_test SET name = '김선호';
SELECT * FROM example.insert_test;
UPDATE example.insert_test SET name = '김선호' WHERE seq in (11, 12, 13, 14, 15); //UPDATE multiple rows
SELECT * FROM example.insert_test;
UPDATE example.insert_test SET name = '요거트', cont = '너무 맛있어' WHERE seq in (11, 12, 13, 14, 15); //UPDATE multiple columns & rows
SELECT * FROM example.insert_test;
```

<br/>

