Function(3) 날짜함수
=============

__1. 현재 날짜와 시간 출력__  

  다양한 SQL 명령으로 현재의 날짜와 시간을 출력할 수 있다.  
  '+0'이라는 연산을 추가하면 날짜나 시간을 형식없이 숫자를 나열한 문자열 형태로 출력.  
  모두 SELECT를 사용.  
    
```
SELECT now(); //2021-09-10 13:48:23
SELECT sysdate();
SELECT current_timestamp();
SELECT curdate(); //2021-09-10
SELECT current_date();
SELECT current_time(); //13:48:23
SELECT now()+0; //20210910134823
SELECT current_time()+0; //134823
```

<br/>

__2. 날짜와 시간에 대한 특정 정보 출력__

```
SELECT dayofweek('2021-09-10 13:48:23'); //요일을 숫자로 출력(1:일요일~7:토요일)
SELECT weekday('2021-09-10 13:48:23'); //요일을 숫자로 출력(0:월요일~6:일요일)
SELECT dayofmonth('2021-09-10 13:48:23'); //일자
SELECT dayofyear('2021-09-10 13:48:23'); //한해의 몇번째 날인지 출력
SELECT month('2021-09-10 13:48:23'); //월
SELECT dayname('2021-09-10 13:48:23'); //요일 영문으로
SELECT monthname('2021-09-10 13:48:23'); //월 영문으로
SELECT quarter('2021-09-10 13:48:23'); //분기
SELECT week('2021-09-10 13:48:23'); //한해의 몇번째 주인지 출력
SELECT year('2021-09-10 13:48:23'); //년도
SELECT hour('2021-09-10 13:48:23'); //시
SELECT minute('2021-09-10 13:48:23'); //분
SELECT second('2021-09-10 13:48:23'); //초
SELECT minute(now());
```

<br/>

__3. 날짜와 시간의 연산__

  date_add(date, interval _expr_ _type_)와 같이 입력.  
  여기서 expr는 type에 따라 입력 형태가 달라진다.  
  
  |type|expr|
  |---|---|
  |second|초|
  |minute|분|
  |hour|시|
  |day|일|
  |month|월|
  |year|년|
  |minute_second|분:초|
  |hour_minute|시:분|
  |hour_second|시:분:초|
  |day_hour|일 시|
  |year_month|년 월|
  |day_minute|일 시:분|
  |day_second|일 시:분:초|
  
```
SELECT date_add('2021-09-10 13:48:23', interval 1 second);
SELECT date_add('2021-09-10 13:48:23', interval 31 day);
SELECT date_add('2021-09-10 13:48:23', interval '1:1' minute_second);
SELECT date_add('2021-09-10 13:48:23', interval '-1 17' day_hour); //하루와 17시간을 뺌
SELECT adddate('2021-09-10 13:48:23', interval '-1 17' day_hour); //결과 동일
SELECT date_sub('2021-09-10 13:48:23', interval '1 17' day_hour); //결과 동일
SELECT subdate('2021-09-10 13:48:23', interval '1 17' day_hour); //결과 동일
```

<br/>

__4. 시간과 초 변환__

```
SELECT sec_to_time(3000); //초 to 시간
SELECT time_to_sec('20:21:30'); //시간 to 초
```

<br/>

__5. period_add, period_diff__

  입력한 년월 데이터에 원하는 개월 수를 더하거나 뺀 값을 'YYYYMM' 형태로 출력.  

```
SELECT period_add(2109, 15);
SELECT period_add(202109, 15);
```

<br/>

__6. date_format__

  SELECT date_format('date', 'format') 형태로 사용함.  
  format에 들어가는 변수에 따라서 출력되는 데이터가 달라짐.  
  
``` 
SELECT date_format('2021-08-09 13:48:23', '%W'); //Monday
SELECT date_format('2021-08-09 13:48:23', '%w'); //1
SELECT date_format('2021-08-09 13:48:23', '%a'); //Mon
SELECT date_format('2021-08-09 13:48:23', '%D'); //9th
SELECT date_format('2021-08-09 13:48:23', '%d'); //09
SELECT date_format('2021-08-09 13:48:23', '%e'); //9
SELECT date_format('2021-08-09 13:48:23', '%m'); //08
SELECT date_format('2021-08-09 13:48:23', '%c'); //8
SELECT date_format('2021-08-09 13:48:23', '%b'); //Aug
SELECT date_format('2021-08-09 13:48:23', '%Y'); //2021
SELECT date_format('2021-08-09 13:48:23', '%y'); //21
SELECT date_format('2021-08-09 13:48:23', '%j'); //221
SELECT date_format('2021-08-09 13:48:23', '%U'); //36
SELECT date_format('2021-08-09 13:48:23', '%H'); //13
SELECT date_format('2021-08-09 13:48:23', '%k'); //13
SELECT date_format('2021-08-09 13:48:23', '%h'); //01
SELECT date_format('2021-08-09 13:48:23', '%l'); //1
SELECT date_format('2021-08-09 13:48:23', '%I'); //01
SELECT date_format('2021-08-09 13:48:23', '%i'); //48
SELECT date_format('2021-08-09 13:48:23', '%r'); //01:48:23 PM
SELECT date_format('2021-08-09 13:48:23', '%T'); //13:48:23
SELECT date_format('2021-08-09 13:48:23', '%S'); //23
SELECT date_format('2021-08-09 13:48:23', '%p'); //PM
```
