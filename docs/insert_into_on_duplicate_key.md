Insert into on duplicate key
=============

__0. 테스트용 데이터 생성__

```
CREATE TABLE example.insert_test3(
	seq int(10) not null primary key,
    cont text null,
    name varchar(15) null,
    tel_num int null,
    input_date datetime null);
INSERT INTO example.insert_test3 (seq, cont, name, tel_num, input_date) VALUES (1, '대한민국', '홍길동', 01012345678, now());
INSERT INTO example.insert_test3 (seq, cont, name, tel_num, input_date) VALUES (2, '대한민국', '홍길동', 01012345678, now());
INSERT INTO example.insert_test3 (seq, cont, name, tel_num, input_date) VALUES (3, '대한민국', '홍길동', 01012345678, now());
INSERT INTO example.insert_test3 (seq, cont, name, tel_num, input_date) VALUES (4, '대한민국', '홍길동', 01012345678, now());
INSERT INTO example.insert_test3 (seq, cont, name, tel_num, input_date) VALUES (5, '대한민국', '홍길동', 01012345678, now());
SELECT * FROM example.insert_test3;

CREATE TABLE example.insert_test4(
	seq int(10) not null,
    cont text null,
    name varchar(15) null,
    tel_num int null,
    input_date datetime null);
INSERT INTO example.insert_test4 (seq, cont, name, tel_num, input_date) VALUES (4, '코로나', '강낭콩', 01098765432, now());
INSERT INTO example.insert_test4 (seq, cont, name, tel_num, input_date) VALUES (5, '코로나', '강낭콩', 01098765432, now());
INSERT INTO example.insert_test4 (seq, cont, name, tel_num, input_date) VALUES (6, '코로나', '강낭콩', 01098765432, now());
INSERT INTO example.insert_test4 (seq, cont, name, tel_num, input_date) VALUES (7, '코로나', '강낭콩', 01098765432, now());
SELECT * FROM example.insert_test4;
```

__1. Insert into on duplicate key란__  

  오라클의 merge문에 해당하는 기능.  
  어떤 데이터를 입력할 때 대상 테이블에 해당 키 데이터가 없으면 insert문을 실행하고,  
  해당 키 데이터가 이미 있는 경우에는 update하여 값을 갱신.  
  
<br/>

__2. 기본사용예시__

  (1) 테이블을 merge 할 경우
  
  INSERT INTO <업데이트할 테이블 1>  
  SELECT * FROM <업데이트에 쓰일 테이블 2>  
  ON DUPLICATE KEY UPDATE <칼럼명 1> = <칼럼명 2>;  //key가 중복될 경우 무엇을 update 할지 명시  
  
```
INSERT INTO example.insert_test3 
SELECT * FROM example.insert_test4 b
ON DUPLICATE KEY UPDATE cont = b.cont, 
                        name = b.name,
                        tel_num = b.tel_num,
                        input_date = now();
SELECT * FROM example.insert_test3;
```

<br/>

  (2) 데이터를 넣어줄 경우
  
  INSERT INTO <업데이트할 테이블 1>  
  VALUES <각 칼럼값>  
  ON DUPLICATE KEY UPDATE <칼럼명 1> = <칼럼값>;  
  
```
INSERT INTO example.insert_test3
VALUES (2, '바보', '냠냠', 01011111111, now())
ON DUPLICATE KEY UPDATE cont = '바보',
                        name = '냠냠',
                        tel_num = 01011111111,
                        input_date = now();
SELECT * FROM example.insert_test3;
```

<br/>
