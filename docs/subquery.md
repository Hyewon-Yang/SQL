Sub query
=============

__1. 서브쿼리의 개념__  

  서브쿼리란, SQL 내에서 또다른 SELECT절을 사용하는 문법.  
  메인쿼리 안에 서브쿼리가 들어있는 형태.  
  하지만 가능하다면 join 을 이용하는 것이 대부분 SQL에서 좋은 성능을 나타냄.  
  
  메인쿼리의 SELECT절, FROM절, WHERE절 중 어디에 사용하느냐에 따라 종류가 다름.  
  
  SELECT절: 스칼라 서브쿼리(Scalar subquery)  
  FROM절: 인라인 뷰(Inline view)  
  WHERE절: 중첩 서브쿼리 / 서브쿼리  
  
<br/>

__2. 스칼라 서브쿼리__

  SELECT로 시작한 후에 '(SELECT ~' 로 시작하는 서브쿼리 삽입.  
  스칼라 서브쿼리의 WHERE절에 메인쿼리의 칼럼값을 넣어, 이 값으로 서브쿼리에서 검색된 값을 출력함.  
  쿼리 결과가 하나의 행으로 나와야 실행할 수 있다.  

```
SELECT * FROM example.student;
SELECT * FROM example.major;

SELECT name as 학생이름,
	(SELECT major_title
    FROM example.major b
    WHERE b.major_id = a.major_id) as 학과명
FROM example.student a;
//student에 있는 major_id 값을 major에서 검색하여 학과명을 가져와 메인쿼리에서 출력

SELECT major_title as 학과명,
	(SELECT name
    FROM example.student b
    WHERE b.major_id = a.major_id) as 학생이름
FROM example.major a;
//반대로 major에 있는 major_id 값을 student에서 검색하여 학생이름을 출력하면?
//major_id가 같은 학생이 여러명 존재하기 때문에 출력 불가
```

<br/>

__3. 인라인 뷰__

  FROM절에 '(SELECT ~'절 삽입.  
  하나의 테이블이라고 생각하고 사용, join이나 where절에 조건절로도 사용 가능.  
  단, 메인쿼리에서 SELECT절이나 WHERE절에 사용하려면 인라인 뷰의 SELECT절에 칼럼명을 적어줘야함.  
  
```
SELECT a.name as 학생이름, b.major_title as 학과명
FROM example.student a, (SELECT major_title, major_id FROM example.major) b
WHERE a.major_id = b.major_id;
//스칼라 서브쿼리와 같은 결과

SELECT a.name as 학생이름, b.major_title as 학과명
FROM example.student a, example.major b
WHERE a.major_id = b.major_id;
//JOIN을 사용할 경우
```

<br/>

__4. 서브쿼리__

  WHERE절에 '(SELECT ~'절 삽입.  
  단일행 서브쿼리(= 쿼리결과가 하나의 행으로 나오는 경우)일 때는 비교연산자 사용할 수 있음.  
  
  |연산자|의미|
  |------|----|
  |=|같다|
  |<>|같지 않다|
  |>|크다|
  |>=|크거나 같다|
  |<|작다|
  |<=|작거나 같다|
  
  복수행 서브쿼리(= 쿼리결과가 복수행으로 나오는 경우)일 때는 다음과 같은 연산자 사용 가능.  
  
  |연산자|의미|
  |------|----|
  |IN (NOT IN)|포함함 (포함하지 않음)|
  |EXIST|서브쿼리의 값이 있을 경우 반환함|
  |NOT EXIST|서브쿼리의 값이 없을 경우 반환함|
  
```
SELECT name as 학생이름
FROM example.student
WHERE major_id = (SELECT major.major_id FROM example.major WHERE major_title = '컴퓨터공학과');
//단일행 서브쿼리

SELECT name as 학생이름
FROM example.student
WHERE major_id IN (SELECT major.major_id FROM example.major WHERE major_title IN ('컴퓨터공학과', '국문학과'));
//복수행 서브쿼리
```
 
