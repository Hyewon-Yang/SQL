SELECT
=============

__0. Terms__  

  Selection: 데이터베이스의 테이블에서 원하는 row만 가지고 오는 것  
  Projection: 데이터베이스의 테이블에서 원하는 column만 가지고 오는 것  
  
<br/>

__1. 실습 데이터 생성__  
  
  데이터베이스와 테이블 생성 후 데이터 insert
  
  
```
CREATE DATABASE kmong;
CREATE TABLE select_test(name varchar(50), dept_cd varchar(1), phone varchar(15), address varchar(100)) character set utf8;
INSERT INTO kmong.select_test (name, dept_cd, phone, address) VALUES ('John', 'A', '01012334455', 'Seoul');
INSERT INTO kmong.select_test (name, dept_cd, phone, address) VALUES ('Sally', 'A', '01019847378', 'Daejeon');
INSERT INTO kmong.select_test (name, dept_cd, phone, address) VALUES ('Tom', 'B', '01023458796', 'Daegu');
INSERT INTO kmong.select_test (name, dept_cd, phone, address) VALUES ('Harry', 'C', '0107777777', 'Pusan');
INSERT INTO kmong.select_test (name, dept_cd, phone, address) VALUES ('Mary', 'D', '01012314244', 'Incheon');
INSERT INTO kmong.select_test (name, dept_cd, phone, address) VALUES ('Kim', 'D', '01087769965', 'Jeju');
```

<br/>

__2. DESC (describe)__

  테이블에 속한 column을 조회
  
```
DESC select_test;
```

<br/>

__3. SELECT__

  \* (아스타)를 사용하면 해당 테이블의 모든 column data 를 출력  
  SELECT 뒤에 특정 column명을 써주면 그 column에 해당하는 data 만 출력  
  FROM 뒤에는 테이블명을 써준다.
    
  
```
SELECT * FROM kmong.select_test;
SELECT name, phone FROM select_test;
```

<br/>

__4. WHERE__

  특정한 조건을 만족하는 row 만 출력하는 경우에 사용

```
SELECT * FROM kmong.select_test
WHERE dept_cd = 'A';
```

<br/>

__5. 표현식(Expression)__

  column data 외에 문자열 등 다른 내용을 출력하고 싶을 때 사용  
  '님 안녕하세요!!' 라는 새로운 column이 추가되어 출력됨.  
  이때, column명 대신 별칭(alias)을 사용하고 싶을 경우 as 를 넣어준다.
  
```
SELECT name, '님 안녕하세요!!' FROM kmong.select_test;
SELECT name as 이름, '님 안녕하세요!!' as 인사문구 FROM select_test;
```

<br/>

__6. DISTINCT__

  중복된 값을 제외하고 출력
  
```
SELECT dept_cd FROM kmong.select_test;
SELECT DISTINCT dept_cd FROM kmong.select_test;
```

<br/>

__7. concat__

  여러 column의 값이나 표현식을 연결해서 하나의 column으로 출력하는 함수
  
```
SELECT concat(name, '의 부서코드는 ', dept_cd, ' 입니다.') FROM kmong.select_test;
SELECT concat(name, '의 부서코드는 ', dept_cd, ' 입니다.') 
FROM kmong.select_test
WHERE name = 'John';
```
