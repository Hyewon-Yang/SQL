Functions
=============

__0. SQL 함수의 분류__  

  DBMS에서 함수를 분류하는 기준에는 여러가지가 있다.  
  * 내장함수와 사용자정의함수  
    : 내장함수는 RDBMS에 이미 내장된 함수이며, 사용자정의함수는 CREATE FUNCTION 을 사용해서 유저가 직접 만든 함수  
  * 단일행함수와 복수행함수  
    : 단일행함수는 한 행의 값을 받아서 특정한 규칙을 통해 변환시키는 함수이고, 복수행함수는 여러 행의 값을 한꺼번에 받아서 하나의 행의 결과값으로 변환하는 함수, count()가 가장 대표적인 복수행함수의 예이다.  
  * 문자함수, 숫자함수, 날짜함수, 형변환함수, 일반함수 등으로도 분류 가능  
  
<br/>

__1. 실습 데이터 생성__  
  
```
CREATE TABLE kmong.country(country_name varchar(100), capital_city varchar(100), continent varchar(100)) character set utf8;
INSERT INTO kmong.country (country_name, capital_city, continent) VALUES ('USA', 'Washington', 'America');
INSERT INTO kmong.country (country_name, capital_city, continent) VALUES ('England', 'London', 'Europe');
INSERT INTO kmong.country (country_name, capital_city, continent) VALUES ('South Korea', '  Seoul', 'Asia');
INSERT INTO kmong.country (country_name, capital_city, continent) VALUES ('Australia', 'Canberra  ', 'Oceania');
INSERT INTO kmong.country (country_name, capital_city, continent) VALUES ('Ghana', 'Accra', 'Africa');
INSERT INTO kmong.country (country_name, capital_city, continent) VALUES ('Argentina', 'Buenos aires', 'America');
SELECT * FROM kmong.country;
```

<br/>

__2. lower/upper__

  입력된 문자를 소문자 또는 대문자로 바꾸는 함수  
  lower(column name), upper(column name)  
  
```
SELECT country_name as 원본, lower(country_name) as 소문자, upper(country_name) as 대문자 FROM kmong.country;
```

<br/>

__3. length__

  데이터의 길이를 반환  
  length(column name)
  
```
SELECT country_name, length(country_name) as 길이 FROM kmong.country;
```

<br/>

__4. concat__

  concat 도 마찬가지로 문자함수로 분류.  
  concat(column name, '문자열', ...)
  
```
SELECT concat(country_name, ' 의 수도는 ', capital_city, ' 입니다!') as 수도소개 FROM kmong.country;
```

<br/>

__5. substr/mid/substring__

  substr, mid, substring은 column의 특정 부분을 출력할 때 사용하며 사용법은 동일함.  
  substr(column name, 시작 위치, 리턴값의 길이)
  
```
SELECT continent as 원본, substr(continent, 2, 2) as substr, mid(continent, 2, 2) as mid, substring(continent, 2, 2) as continent 
FROM kmong.country;
```

<br/>

__6. instr__

  특정 문자열의 위치를 숫자로 리턴. 가장 처음 발견되는 위치를 출력하며, 대소문자 구별하지 않음.  
  instr(column name, '찾는 문자')
  
```
SELECT continent as 원본, instr(continent, 'A') as instr FROM kmong.country;
```

<br/>

__7. lpad/rpad__

  어떤 데이터가 기준보다 짧은 경우에 원하는 문자를 왼쪽이나 오른쪽에 채워 자릿수를 맞춰주는 함수.  
  lpad(column name, 기준자릿수, 채워넣을 숫자나 문자)
  
```
SELECT continent as 원본, lpad(continent, 10, 'A') as lpad, rpad(continent, 10, 'A') as rpad FROM kmong.country;
```

<br/>

__8. trim/ltrim/rtrim__

  trim은 문자열의 양쪽 공백을 없애는 함수, ltrim과 rtrim은 각각 왼쪽, 오른쪽 공백을 없애는 함수.  
  trim(column name)
  
```
SELECT capital_city as 원본, trim(capital_city) as trim, ltrim(capital_city) as ltrim, rtrim(capital_city) as rtrim 
FROM kmong.country;
```

<br/>

__9. replace__

  특정 문자열을 찾아서 다른 문자열로 치환, 대소문자 구별함.  
  replace(column name, '찾을 문자', '치환할 문자')
  
```
SELECT continent as 원본, replace(continent, 'A', '@') as 'replace' FROM kmong.country;
SELECT continent as 원본, replace(continent, 'a', '#') as 'replace2' FROM kmong.country;
```
