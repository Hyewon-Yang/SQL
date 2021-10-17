Insert
=============

__1. INSERT란__  

  insert는 테이블에 새로운 데이터를 입력하는 명령어.  
  select는 여러 테이블에서 join해와서 출력할 수 있지만 insert는 한번에 하나의 테이블에만 입력할 수 있다.  
  
<br/>

__2. 단일행 입력 (칼럼 미지정)__

  insert 대상 테이블의 칼럼을 지정하지 않고 데이터를 입력하는 방법  
  테이블의 칼럼 생성 순서대로 데이터가 들어감.  
  
```
CREATE TABLE example.insert_test(
	seq int(10) primary key,
    cont text,
    name varchar(15),
    tel_num int(11),
    input_date datetime);
INSERT INTO example.insert_test VALUES (1, '대한민국', '홍길동', 01012345678, now());
SELECT * FROM example.insert_test;
```

<br/>

__3. 단일행 입력 (칼럼 지정)__

  insert 시 테이블명 뒤에 칼럼명을 지정하는 방법. 이 순서대로 데이터를 넣을 수 있음.  
  또한 일부의 데이터만 넣는 것도 가능함. 이 경우 데이터가 없는 칼럼에는 null 이 입력됨.  
  
```
INSERT INTO example.insert_test (seq, cont, name, tel_num, input_date) VALUES (8, '대한민국', '홍길동', 01012345678, now());
SELECT * FROM example.insert_test;
INSERT INTO example.insert_test (seq, cont, input_date) VALUES (10, '대한민국', now());
SELECT * FROM example.insert_test;
```

<br/>

__4. 복수행 입력__

  하나의 insert문으로 여러 행의 데이터를 입력할 수 있음.  
  
```
INSERT INTO example.insert_test VALUES (11, '대한민국', '홍길동', 01012345678, now()),
									(12, '대한민국', '홍길동', 01012345678, now()),
                                    (13, '대한민국', '홍길동', 01012345678, now()),
                                    (14, '대한민국', '홍길동', 01012345678, now()),
                                    (15, '대한민국', '홍길동', 01012345678, now());
SELECT * FROM example.insert_test;
```

<br/>

__5. insert select__

  select 한 결과를 insert 문을 이용해서 입력하는 방법.  
  insert문과 select문을 나란히 쓴 형태.  
  
```
CREATE TABLE example.insert_test2 AS SELECT * FROM example.insert_test WHERE 1=2;
//테이블 복사(1=2는 테이블 형태만 복사, 1=1는 데이터와 형태 모두 복사)

SELECT * FROM example.insert_test2;
INSERT INTO example.insert_test2 VALUES (21, '대한민국', '홍길동', 01012345678, now()),
										(22, '대한민국', '홍길동', 01012345678, now()),
                                        (23, '대한민국', '홍길동', 01012345678, now()),
                                        (24, '대한민국', '홍길동', 01012345678, now()),
                                        (25, '대한민국', '홍길동', 01012345678, now());
SELECT * FROM example.insert_test;
SELECT * FROM example.insert_test2;
INSERT INTO example.insert_test SELECT * FROM example.insert_test2;
SELECT * FROM example.insert_test;
```

<br/>
