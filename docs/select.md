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

<br/>

__8. 산술연산자__

  column data 간의 사칙연산 수행  
  합계와 평균값을 각각 새로운 column으로 추가하여 출력

```
CREATE TABLE kmong.exam_result(name varchar(50), math int(10), english int(10), korean int(10)) character set utf8;
INSERT INTO kmong.exam_result (name, math, english, korean) VALUES ('김', 45, 67, 89);
INSERT INTO kmong.exam_result (name, math, english, korean) VALUES ('박', 98, 87, 82);
INSERT INTO kmong.exam_result (name, math, english, korean) VALUES ('이', 75, 55, 69);
INSERT INTO kmong.exam_result (name, math, english, korean) VALUES ('정', 80, 72, 33);
INSERT INTO kmong.exam_result (name, math, english, korean) VALUES ('최', 79, 84, 75);
INSERT INTO kmong.exam_result (name, math, english, korean) VALUES ('신', 69, 50, 59);
INSERT INTO kmong.exam_result (name, math, english, korean) VALUES ('임', 91, 83, 76);
SELECT * FROM kmong.exam_result;
SELECT name, math, english, korean, math + english + korean as total FROM kmong.exam_result;
SELECT name, math, english, korean, (math + english + korean)/3 as average FROM kmong.exam_result;
```

<br/>

__9. WHERE + 연산자__

  WHERE 절에 다양한 연산자를 사용할 수 있다.  
  비교연산자 외에, BETWEEN a AND b (= a와 b 사이의 값을 검색), IN(a, b, c) (= a, b, c 중 어느 하나인 것을 검색), LIKE (= 특정 패턴을 가지고 있는 조건을 검색), a AND b, a OR b, NOT a 등을 사용할 수 있다.

```
SELECT * FROM kmong.exam_result WHERE korean >= 80;
SELECT * FROM kmong.exam_result WHERE (math + english + korean)/3 >= 80;
SELECT * FROM kmong.exam_result WHERE math BETWEEN 50 AND 70;
SELECT * FROM kmong.exam_result WHERE math > 60 OR korean > 70;
```

<br/>

__10. ORDER BY__

  오름차순으로 데이터 정렬.  
  DESC 사용시 내림차순으로 정렬.  
  문자, 숫자에 모두 적용 가능  
  ORDER BY 뒤에는 column 명이나 연산식을 주로 사용하나, 숫자 하나만 넣을 수도 있음. 이 경우는 해당 순서의 column을 기준으로 정렬하라는 의미.  
  하지만 가독성이 떨어지고 이후 테이블이 수정될 경우를 감안하면 바람직한 방법은 아님.
  
```
SELECT * FROM kmong.exam_result ORDER BY math;
SELECT * FROM kmong.exam_result ORDER BY math DESC;
SELECT * FROM kmong.exam_result ORDER BY (math + english + korean)/3 DESC;
SELECT * FROM kmong.exam_result ORDER BY 3;
```

<br/>

__11. 집합연산자__

  하나의 테이블 또는 하나의 SELECT문으로 나오는 데이터셋을 '집합'으로 표현함.  
  UNION 은 중복값을 제거하고 정렬을 수행한 합집합 연산이고, UNION ALL 은 중복 제거와 정렬을 하지 않는 합집합 연산을 뜻한다.  
  INTERSECT(교집합)과 MINUS(차집합)는 mysql 버전에서 지원하고 있지 않은 기능이지만 다른 sql에서는 사용 가능하므로 알아두면 좋음.
  
```
CREATE TABLE kmong.exam_result_2(name varchar(50), math int(10), english int(10), korean int(10)) character set utf8;
INSERT INTO kmong.exam_result_2 (name, math, english, korean) VALUES ('Amy', 78, 99, 57);
INSERT INTO kmong.exam_result_2 (name, math, english, korean) VALUES ('Jane', 60, 91, 86);
INSERT INTO kmong.exam_result_2 (name, math, english, korean) VALUES ('Bill', 75, 59, 79);
INSERT INTO kmong.exam_result_2 (name, math, english, korean) VALUES ('Silly', 86, 66, 87);
INSERT INTO kmong.exam_result_2 (name, math, english, korean) VALUES ('Mack', 97, 89, 95);
SELECT * FROM kmong.exam_result UNION SELECT * FROM kmong.exam_result_2;
SELECT * FROM kmong.exam_result UNION SELECT * FROM kmong.exam_result;
SELECT * FROM kmong.exam_result UNION ALL SELECT * FROM kmong.exam_result;
```
```
CREATE TABLE math_student (name varchar(50), student_no varchar(10));
CREATE TABLE korean_student (name varchar(50), student_no varchar(10));
INSERT INTO math_student (name, student_no) VALUES ('태연', '111');
INSERT INTO math_student (name, student_no) VALUES ('윤아', '112');
INSERT INTO math_student (name, student_no) VALUES ('수영', '113');
INSERT INTO math_student (name, student_no) VALUES ('써니', '114');
INSERT INTO korean_student (name, student_no) VALUES ('태연', '111');
INSERT INTO korean_student (name, student_no) VALUES ('윤아', '112');
INSERT INTO korean_student (name, student_no) VALUES ('티파니', '201');
INSERT INTO korean_student (name, student_no) VALUES ('유리', '202');
SELECT * FROM kmong.math_student;
SELECT * FROM kmong.korean_student;
SELECT * FROM math_student INTERSECT SELECT * FROM korean_student;
SELECT * FROM math_student MINUS SELECT * FROM korean_student;
```
