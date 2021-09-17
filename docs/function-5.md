Function(5) 일반함수
=============

__0. Data table__

```
CREATE TABLE kmong.salary_table(name varchar(10), dept varchar(1), salary int(5), bonus int(5)) character set utf8;
INSERT INTO kmong.salary_table (name, dept, salary, bonus) VALUES ('박지성', 'A', 100, 200);
INSERT INTO kmong.salary_table (name, dept, salary, bonus) VALUES ('차두리', 'A', 200, 400);
INSERT INTO kmong.salary_table (name, dept, salary, bonus) VALUES ('홍길동', 'B', 300, null);
INSERT INTO kmong.salary_table (name, dept, salary) VALUES ('손흥민', 'B', 150);
INSERT INTO kmong.salary_table (name, dept, salary, bonus) VALUES ('피카추', 'C', 1000, 200);
SELECT * FROM kmong.salary_table;
```

<br/>

__1. ifnull__  

  null인 데이터 값을 다른 특정 값으로 출력하게 하는 함수.  
  ifnull(data, 'null 대신 들어갈 문자나 숫자 또는 컬럼명')  

```
SELECT name, dept, salary, ifnull(bonus, 0) FROM kmong.salary_table;
SELECT name, dept, salary, ifnull(bonus, '해당없음') FROM kmong.salary_table;
SELECT name, dept, salary, ifnull(bonus, name) FROM kmong.salary_table;
```

<br/>

__2. if__

  if(조건, 조건 성립시 출력, 조건 미성립시 출력)  
  null은 비교 연산자를 사용하지 않고 is 나 is not을 사용해야함.  

```
SELECT name, dept, salary, if(bonus is null, '해당없음', bonus) FROM kmong.salary_table;
SELECT name, dept, salary, if(bonus is not null, bonus, '해당없음') FROM kmong.salary_table;
SELECT name, dept, if(salary >= 300, '고액연봉자', '일반연봉자'), bonus FROM kmong.salary_table;
```

<br/>

__3. case__

  여러가지 경우에 대해 출력값이 달라질 때 사용.  

```
SELECT name
     , case when dept = 'A' then '경영지원부'
            when dept = 'B' then '영업부'
            else '회계팀' end as dept //이렇게 끝내면 C, D, E.. 에 대해 모두 '회계팀' 출력
            when dept = 'C' then '회계팀' end as dept //이 경우에는 C일 때만 '회계팀' 출력
     , salary
     , bonus
FROM kmong.salary_table;
```

<br/>

__4. 활용예시__

```
SELECT name
     , case when dept = 'A' then '경영지원부'
            when dept = 'B' then '영업부'
            when dept = 'C' then '회계팀' end as dept
     , salary
     , if(salary >= 300, '고액연봉', '일반') as salary_type
     , ifnull(bonus, 0)
     , case when ifnull(bonus, 0) = 0 then '해당없음'
            else '보너스해당자' end as bonus_type
FROM kmong.salary_table;
```
