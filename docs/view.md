View
=============

__1. View란__

  가상의 테이블 개념. 데이터는 없고 SQL 만 저장되어 있는 object.  
  view를 SELECT하면 view가 가지고 있는 SQL문이 실행된다.  
  SELECT 서브쿼리에서 FROM 절에 들어가는 inline view 와 같은 것.  
  
  view를 따로 만드는 이유는, 어떤 사용자가 특정 테이블에 보안상 접근할 수 없으나 그 테이블 안의 어떤 정보가 필요한 경우 사용 가능.  
  
  기본적으로 일반 테이블과 같은 형태를 가지며, SQL문으로 조작하는 방법도 유사함.  
  기본테이블의 기본키를 포함하여 뷰를 생성하면 삽입, 삭제, 갱신, 연산이 가능함.  
  한번 정의된 뷰는 다른 뷰의 기본데이터가 될 수 있고, 뷰에 정의된 기본테이블이나 뷰를 삭제하면 해당 데이터를 기초로 한 다른 뷰들이 자동으로 삭제됨.  
  뷰의 내용을 수정할 때는 DROP 과 CREATE 를 반복해야 함. (ALTER 사용불가)  
  원본 테이블과 같은 이름을 사용할 수 없으며, 실무에서는 주로 'vw_' 등의 접미사나 접두사를 붙임.  
  
<br/>

__2. View 사용예제__

```
//단일 테이블의 필요한 필드 조회
CREATE VIEW vw_student AS 
SELECT major_id, student_id
FROM example.student
WHERE major_id > 0; //뷰 생성 후에
SELECT * FROM vw_student; //조회

//여러 테이블의 필요한 필드 조회
CREATE VIEW vw_student_major AS
SELECT a.major_id, b.student_id
FROM example.major AS a, example.student AS b
WHERE a.major_id in (9903, 9904);
SELECT * FROM vw_student_major;

//뷰 삭제
DROP VIEW vw_student;
```

<br/>
