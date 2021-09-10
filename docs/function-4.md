Function(4) 형변환함수
=============

__1. MySQL의 데이터 타입__  

  데이터를 저장하고 표현하는 데 문제가 없는 타입 중 가장 작은 것을 고르는 것이 좋다.  
  작은 데이터 타입일수록 디스크나 메모리에 더 적은 공간을 사용하므로 더 빠르며, CPU도 덜 소비한다.  
  컬럼은 되도록 NOT NULL(NULL 허용안함)로 정의하는 것이 좋다. NULL 허용 컬럼은 저장공간을 더 많이 사용하므로, NULL 대신 0이나 특수한 값, 빈 문자열 등을 사용하는 것을 고려하자.
  
  (1) 정수 타입
  
  정수를 저장하기 위해서는 TINYINT, SMALLINT, MEDIUMINT, INT, BIGINT와 같은 정수 타입을 사용할 수 있다.  
  정수 타입에는 UNSIGNED(부호없음) 속성을 사용할 수 있는데, 이는 음수 값을 허용하지 않는 대신 저장가능한 양수 값의 한도를 두 배로 늘려준다.  
  
  |data type|range|byte|
  |---|---|---|
  |TINYINT|-128 ~ 127(signed), 0 ~ 255(unsigned)|1byte|
  |SMALLINT|-32768 ~ 32767(signed), 0 ~ 65535(unsigned)|2bytes|
  |MEDIUMINT|-8388608 ~ 8388607(signed), 0 ~ 16777215(unsigned)|3bytes|
  |INT|-2147483648 ~ 2147483647(signed), 0 ~ 4294967295(unsigned)|4bytes|
  |BIGINT|-9223372036854775808 ~ 9223372036854775807(signed), 0 ~ 18446744073709551615(unsigned)|8bytes|
    
  (2) 실수 타입
  
  실수 타입으로는 소수부가 있는 실수를 표현할 수 있다. 또한 BIGINT로 표현할 수 없을만큼 큰 정수도 DECIMAL을 이용하여 저장 가능하다.  
  보통 DECIMAL 혹은 DOUBLE을 사용하는데, 둘의 차이점은 고정소수점과 부동소수점의 차이이다.  
  
  __DECIMAL__ 은 고정소수점으로, 소수부를 정확하게 저장하는 용도로 사용한다.(예: 3.4)  
  DECIMAL(M, D): M은 소수부를 포함한 실수의 총 자릿수(최대 65), D는 소수부의 자릿수(0이면 소수부 없음)  
  DEC, NUMERIC이라고 쓰기도 함.  
  
  __DOUBLE__ 은 부동소수점으로, 대략적인 근사값을 표현할 때 사용한다.(예: 1.2E3)  
  DOUBLE에서 대략 15자리까지만 정확하다.  
  DOUBLE(M, D): M은 소수부를 포함한 실수의 총 자릿수, D는 소수부의 자릿수  
  DOUBLE PRECISION, REAL로 쓰기도 함.  
  
  *고정소수점, 부동소수점에 대한 설명은 https://gsmesie692.tistory.com/94 참고
  
  (3) 문자열 데이터 타입
  
  문자열 데이터 타입에서는 CHAR와 VARCHAR의 차이를 이해하는 것이 중요하다.  
  
  __VARCHAR()__ 는 가변 길이의 문자열을 저장하는 가장 흔한 문자열 데이터 타입으로, 필요한 만큼만 공간을 사용하므로 저장 공간을 적게 사용할 수 있다.  
  문자마다 사용하는 바이트 수가 다른 복잡한 문자셋을 사용할 때 유용함.  
  VARCHAR(20)인 column에 10자만 저장하면, 실제로 10자만큼의 메모리를 차지.  
  
  __CHAR()__ 는 고정 길이를 갖는 문자열을 저장하며, 아주 짧은 문자열을 저장할 때나 모든 값이 거의 같은 길이일 때 유용함.  
  CHAR(20)인 column에 10자만 저장해도 20자만큼의 메모리를 차지.  
    
  그 외, 텍스트 형식(TEXT)은 크기에 따라 아래와 같이 나눌 수 있다.  
    
  |data type|byte|
  |---|---|
  |TINYTEXT(M)|최대 255(2^8-1) bytes|
  |TEXT(M)|최대 65535(2^16-1) bytes(약 64KB)|
  |MEDIUMTEXT(M)|최대 2^24-1 bytes(약 16MB)|
  |LONGTEXT(M)|최대 2^32-1 bytes(약 4GB)|

 (4) 날짜 및 시간 타입
 
 |data type|range|
 |---|---|
 |DATE|1001-01-01 ~ 9999-12-31|
 |TIME|-838:59:59 ~ 838:59:59|
 |DATETIME|1001-01-01 00:00:00 ~ 9999-12-31 23:59:59|
 |TIMESTAMP|1970-01-01 00:00:00 이후로 지난 초(2038년 이내)|
 |YEAR|1901 ~ 2155|
 
 
 (5) 이진형 데이터 타입
 
 |data type|definition|
 |---|---|
 |BINARY(M)|CHAR형태의 이진 데이터 타입, 이진 데이터를 문자열로 저장|
 |VARBINARY(M)|VARCHAR형태의 이진 데이터 타입, 이진 데이터를 문자열로 저장|
 |TINYBLOB(M)|최대 255(2^8-1) bytes|
 |BLOB(M)|최대 65535(2^16-1) bytes(약 64KB)|
 |MEDIUMBLOB(M)|최대 2^24-1 bytes(약 16MB)|
 |LONGBLOB(M)|최대 2^32-1 bytes(약 4GB)|
 
 <br/>
 
__2. 묵시적 형변환__

  데이터의 형태를 사용자의 의도에 맞게 데이터베이스가 자체적으로 형변환을 하여 결과를 출력하는 것.  
  
```
SELECT 100 + 200;
SELECT '100' + '200'; //문자로 입력해도 숫자처럼 연산 가능
SELECT concat(1, '은 내 번호'); //숫자와 문자를 합치는 것도 가능
```

<br/>

__3. cast, convert__

  데이터 타입을 변환시켜주는 형변환 함수.  
  CAST(data as type(len));  
  CONVERT(data, type(len));  
  
```
SELECT cast(100 as char) as num_to_char, cast('100' as signed) as char_to_num;
SELECT cast(now() as signed);
SELECT convert(now(), signed);
SELECT cast(20210910 as DATE);
```
