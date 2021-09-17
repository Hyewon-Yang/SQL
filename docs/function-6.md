Function(6) 복수행함수
=============

__0. Data table__

  복수행 함수는 단일행 함수와 다르게 한번에 여러 데이터에 대한 결과를 출력한다.  
  복수행 함수는 window 함수라고도 하고 그룹함수라고도 부른다.  
  데이터 테이블은 앞서 function(5)에서 사용한 것을 그대로 사용.  

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

__1. count__

  입력되는 데이터의 총 수를 반환하는 함수.  
  '*' 을 넣으면 전체 칼럼에 대해서, 특정 칼럼명을 넣으면 해당 칼럼에서 null을 제외한 값의 수를 반환.  

```
SELECT count(*) FROM salary_table;
SELECT count(bonus) FROM salary_table;
```

<br/>

__2. sum, avg__

  복수행 함수 안에 들어가는 칼럼 중 null이 포함되어 있다면 null 값은 제외하고 결과가 계산됨을 주의.  
  null 값을 포함해서 전체에 대해 계산하고 싶다면 null값을 다른 값으로 처리해줘야함.  
  
```
SELECT sum(salary) FROM salary_table;
SELECT avg(bonus) FROM salary_table;
SELECT avg(ifnull(bonus, 0)) FROM salary_table;
```

<br/>

__3. max, min__

```
SELECT max(salary), min(salary) FROM salary_table;
```

<br/>

__4. stddev, variance__

```
SELECT stddev(salary) FROM salary_table;
SELECT variance(salary) FROM salary_table;
```

<br/>

__5. group by__

  새로운 데이터셋 생성.  

```
CREATE DATABASE example;
CREATE TABLE example.budget(do varchar(100) null, city varchar(100) null, budget_value int null, population int null);
INSERT INTO example.budget (do, city, budget_value, population) VALUES ('서울특별시', '서울특별시', 23324, 345);
INSERT INTO example.budget (do, city, budget_value, population) VALUES ('부산광역시', '부산광역시', 34323, 5345);
INSERT INTO example.budget (do, city, budget_value, population) VALUES ('경상남도', '창원시', 4331, 435);
INSERT INTO example.budget (do, city, budget_value, population) VALUES ('경상남도', '양산시', 25436, 2134);
INSERT INTO example.budget (do, city, budget_value, population) VALUES ('경상남도', '밀양시', 62341, 6523);
INSERT INTO example.budget (do, city, budget_value, population) VALUES ('경기도', '부천시', 3242, 345);
INSERT INTO example.budget (do, city, budget_value, population) VALUES ('경기도', '시흥시', 3245, 546);
INSERT INTO example.budget (do, city, budget_value, population) VALUES ('경기도', '수원시', 3234, 345);
INSERT INTO example.budget (do, city, budget_value, population) VALUES ('충청남도', '공주시', 2425, 436);
INSERT INTO example.budget (do, city, budget_value, population) VALUES ('충청남도', '논산시', 5534, 4567);
INSERT INTO example.budget (do, city, budget_value, population) VALUES ('강원도', '속초시', 6542, 3542);
INSERT INTO example.budget (do, city, budget_value, population) VALUES ('강원도', '강릉시', 2342, 4355);
INSERT INTO example.budget (do, city, budget_value, population) VALUES ('강원도', '태백시', 5465, 45);
INSERT INTO example.budget (do, city, budget_value, population) VALUES ('전라북도', '전주시', 456, 645);
INSERT INTO example.budget (do, city, budget_value, population) VALUES ('전라북도', '군산시', 3243, 234);
SELECT * FROM example.budget;
```

  각 도시의 budget_value의 평균과 합을 광역시도별로 묶어서 출력.  
  
```
SELECT do, avg(budget_value) as 예산평균, sum(budget_value) as 예산합계
FROM example.budget
GROUP BY do;
```

  group by 절에 함수를 사용할 수 있음. 단, 이때는 select 절에도 group by 절에서 쓴 함수를 그대로 써줘야 정상적으로 작동함.  

```
SELECT do, avg(budget_value) as 예산평균, sum(budget_value) as 예산합계
FROM example.budget
GROUP BY if(do in ('서울특별시', '경기도'), '수도권', '지방');
```
```
SELECT if(do in ('서울특별시', '경기도'), '수도권', '지방') as 지역구분, 
avg(budget_value) as 예산평균, sum(budget_value) as 예산합계
FROM example.budget
GROUP BY if(do in ('서울특별시', '경기도'), '수도권', '지방');
```

  서울특별시와 경기도에 해당하는 do 칼럼을 수도권으로 묶고 기타 지역은 지방으로 나누어 평균값과 합을 출력할 것.  
  하지만 위의 코드는 의도한 결과대로 나오지 않고, 아래 코드처럼 해야 정상적으로 작동함.  
  group by 절과 select 절에 동일한 형태의 함수를 작성해줘야 함!!  
  
  
  
