DDL
=============

__1. DDL이란__  

  Data Definition Language, DB 내의 여러 object를 생성, 변경, 관리하는 문장.  
  |DDL 명령어|정의|
  |---|---|
  |CREATE|새로운 오브젝트를 생성|
  |ALTER|이미 존재하는 오브젝트의 내용 변경|
  |TRUNCATE|테이블의 데이터를 모두 삭제하고 차지하고 있던 공간을 반납|
  |DROP|테이블자체를 삭제, 인덱스까지 모두 삭제|
  
<br/>

__2. CREATE__

  Table, function, index, user 등 대부분의 MySQL 오브젝트를 생성할 수 있음.  
  대표적으로 CREATE TABLE 예제를 살펴보면,  
  
  CREATE TABLE 스키마명.테이블명(  
    <칼럼명> <데이터타입> <칼럼정보>  
    ...  
    primary key <칼럼명>  
    ) engine;  
    
  필수는 아니지만 디테일한 칼럼정보를 지정해줄 수 있는데,  
  not null: 이 칼럼에는 null 이 허용되지 않음. 어떤 값이라도 반드시 존재해야 함. insert시 해당 칼럼에 값을 넣지 않으면 에러 발생.  
  null: 이 칼럼에는 null 을 허용함.
  comment: 칼럼 또는 테이블에 코멘트(논리명)를 부여  
  primary key: 해당 테이블의 primary key 설정. 단, PK로 설정하는 칼럼은 not null 로 정의되어야함.  
  engine: MySQL 에 존재하는 두가지 테이블 스토리지 엔진(InnoDB, MyISAM) 중 어떤 것으로 데이터를 저장할지 선택.  
    
```
CREATE TABLE example.com_com_c(
	CD_NM 			varchar(100) not null comment '코드명',
    KOR_CD_NM 		varchar(100) not null comment '한글코드명',
    COM_CD_TYP_CD	varchar(3) not null comment '공통코드유형코드',
    UPR_CD_NM 		varchar(100) null comment '상위코드명',
    CD_TBL_NM 		varchar(100) null comment '코드테이블명',
    USE_YN 			varchar(1) not null comment '사용여부',
    RGST_DTM 		datetime not null comment '등록일시',
    RGSTR_ID 		varchar(30) not null comment '등록자 ID',
    UPD_DTM 		datetime not null comment '수정일시',
    UPDR_ID			varchar(30) not null comment '수정자 ID',
    UPD_PRGM_ID 	varchar(50) not null comment '수정프로그램 ID',
		primary key (CD_NM)
        ) comment '공통_공통코드' engine = InnoDB;
```

<br/>

__3. ALTER__

  다양한 오브젝트를 수정, 변경할 수 있으나 테이블 내 칼럼에 대한 수정구문으로 예시를 들면,  
  
```
ALTER TABLE example.com_com_c MODIFY UPD_DTM datetime default current_timestamp() null; //not null to null
ALTER TABLE example.com_com_c CHANGE USE_YN USE_YESNO varchar(1) not null; //칼럼명 변경
ALTER TABLE example.com_com_c MODIFY UPR_CD_NM varchar(100) null comment '칼럼코멘트'; //칼럼코멘트 변경
ALTER TABLE example.com_com_c ADD NEW_COLUMN int null after UPDR_ID; //신규 칼럼 추가
ALTER TABLE example.com_com_c MODIFY UPD_PRGM_ID int not null; //칼럼 데이터타입 변경
```

<br/>

__4. TRUNCATE__

  테이블의 데이터를 삭제하고 해당 테이블이 차지하고 있던 디스크 공간을 반납.  
  MySQL 에서는 오라클과 달리 TRUNCATE시 인덱스가 drop 되지 않는다.  
  테이블을 drop했다가 다시 create한다는 점에서 DELETE와 다른데, DELETE보다 전체 데이터를 삭제할 때는 더 빠르나 데이터 복구가 불가능하다는 단점이 있음.  

```
TRUNCATE TABLE example.com_com_c;
SELECT * FROM example.com_com_c;
```

<br/>

__5. DROP__

  해당 테이블의 row는 물론이고 인덱스와 저장공간 모두 반납됨.  
  
```  
DROP TABLE example.com_com_c;
SELECT * FROM example.com_com_c; //에러발생
```

<br/>
