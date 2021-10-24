Constraints
=============

__1. 제약조건이란__

  제약조건(Constraint)란, DB 내 테이블에 정해둔 어떤 규칙에 따라 올바른 데이터만 입력받을 수 있도록 하는 기능.  
  제약조건을 활용하면 데이터의 정확성과 신뢰도를 확보할 수 있음.  
  MySQL 에서 지원하는 제약조건은 크게 여섯가지,  
  - primary key  
  - foreign key  
  - not null  
  - unique  
  - check  
  - default  
  
  테이블을 생성하는 단계에서 DDL문에 포함하여 생성할 수도 있고, 이후에 칼럼에 추가하거나 변경, 삭제도 가능.  
  요즘 실무에서는 foreign key 를 잘 쓰지 않는 추세라고 함.  
  
<br/>

__2. Primary key__

  각 row를 특정할 수 있는 구분키로, 테이블 내 모든 데이터 간의 유일성을 보장하는 칼럼에 설정한다.  
  테이블 당 primary key는 하나만 생성 가능하며, primary key 를 구성하는 칼럼은 복수로 설정 가능.  
  중복을 막고, null 을 허용하지 않으므로 unique + not null 의 의미를 가짐.  

```
SELECT * FROM example.student;
ALTER TABLE example.student
		ADD primary key (student_id); //ADD
ALTER TABLE example.student DROP primary key; //DROP
```

<br/>

__3. Foreign key__

  어떤 테이블의 칼럼 값이 다른 테이블의 칼럼 값을 참조할 때 사용하는 제약조건.  
  예를 들어 쇼핑몰의 주문 테이블에 있는 고객 ID 칼럼에 들어오는 값은 고객 테이블에 저장된 고객 ID 값 중 하나가 들어와야 함.  
  즉, 고객 테이블의 고객 ID에 존재하지 않는 고객 ID값은 주문 테이블의 고객 ID 칼럼에 들어갈 수 없음을 뜻한다.  
  
```
SELECT * FROM example.major;
ALTER TABLE example.major
		ADD primary key (major_id);
ALTER TABLE example.student
		ADD CONSTRAINT student_major_id_fk
			foreign key (major_id) references example.major (major_id);
ALTER TABLE example.student DROP foreign key student_major_id_fk;
```

<br/>

__4. Not null__

  어떤 칼럼에 null 값이 들어올 수 없음을 명시한 제약조건.  
  반드시 필요한 정보가 담길 칼럼에 사용한다.  
  
```
ALTER TABLE example.student MODIFY student_ID int not null;
ALTER TABLE example.student MODIFY student_ID int null;
```

<br/>

__5. Unique__

  어떤 칼럼에 중복된 값이 들어가지 못하게 설정하는 제약조건.  
  primary key 를 제외한 칼럼 중에 중복된 값이 들어오면 안되는 경우에 사용.  
  칼럼 두개를 하나의 unique 제약조건에 사용하는 경우, 하나씩 중복 체크하는 것이 아니라 설정한 두 칼럼의 값이 모두 같아야 제약조건에 걸리게 됨.  
  
```
ALTER TABLE example.student
		ADD CONSTRAINT student_pk
			unique (student_id, major_id);
ALTER TABLE example.student DROP KEY student_pk;
```

<br/>

__6. Check__

  어떤 칼럼에 지정된 값 이외의 다른 값이 들어오지 못하도록 하는 제약조건.  
  몇개의 값만 들어오는 코드성 칼럼, Y/N 값이 들어오는 칼럼, 어떤 범위 내의 값만 들어오는 칼럼 등에 사용.  

```
SELECT * FROM example.customer;
ALTER TABLE example.customer
	ADD CONSTRAINT CHK_point CHECK (point >= 5); //조건을 만족하지 못하면 에러 발생
ALTER TABLE example.customer DROP CONSTRAINT CHK_point;
```

<br/>

__7. Default__

  특정 값을 입력하지 않았을 때 기본적으로 row가 생기면서 들어가는 초기값을 설정함.  
  
```
ALTER TABLE example.customer ALTER column name SET default 'N';
ALTER TABLE example.customer ALTER column name DROP default;
```

<br/>
