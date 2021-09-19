JOIN
=============

__0. 실습 데이터 생성__  

```
CREATE TABLE example.student (
	student_id int(10) comment '학생번호',
    major_id int(10) comment '학과ID',
    bl_prfs_id int(10) comment '담당교수ID',
    name varchar(20) comment '학생이름',
    tel varchar(15) comment '학생연락처'
    );
CREATE TABLE example.professor (
	prfs_id int(10) comment '교수ID',
    bl_major_id int(10) comment '소속학과ID',
    name varchar(20) comment '교수이름',
    tel varchar(15) comment '교수연락처'
    );
CREATE TABLE example.major (
	major_id int(10) comment '학과ID',
    major_title varchar(30) comment '학과명',
    major_prfs_cnt int(5) comment '학과소속교수수',
    major_student_cnt int(5) comment '학과소속학생수',
    tel varchar(15) comment '학과사무실연락처'
    );
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1001, 9901, 7029901, '한지호', '01098447362');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1002, 9902, 7029902, '김은숙', '01023456787');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1003, 9903, 7039903, '강경호', '01092938476');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1004, 9904, 7049904, '민현민', '01088786623');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1005, 9905, 7059905, '조승우', '01092877795');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1006, 9901, 7069901, '이남철', '01045671234');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1007, 9902, 7079902, '이강철', '01021213434');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1008, 9903, 7089903, '조민수', '01098937262');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1009, 9904, 7099904, '박찬경', '01029884432');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1010, 9905, 7109905, '이도경', '01029385647');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1011, 9901, 7019901, '이만호', '01099996453');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1012, 9902, 7029902, '김효민', '01092887666');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1013, 9903, 7039903, '최효성', '01098999933');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1014, 9904, 7049904, '우민국', '01087651112');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1015, 9905, 7059905, '지대한', '01093934848');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1016, 9901, 7069901, '한나름', '01023329882');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1017, 9902, 7079902, '유육경', '01099881111');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1018, 9903, 7089903, '조민경', '01023311120');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1019, 9904, 7099904, '경지수', '01029100293');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1020, 9905, 7109905, '오종환', '01098882226');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1021, 9901, 7019901, '조형민', '01098909876');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1022, 9902, 7029902, '이수강', '01099992222');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1023, 9903, 7039903, '서민호', '01092997654');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1024, 9904, 7049904, '박효숙', '01022293332');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1025, 9905, 7059905, '남궁옥경', '01099938475');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1026, 9901, 7069901, '피경남', '01029222233');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1027, 9902, 7079902, '고주경', '01099226655');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1028, 9903, 7089903, '하지만', '01022228965');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1029, 9904, 7099904, '기지효', '01012090912');
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1030, 9905, 7109905, '박민호', '01074746363');
INSERT INTO example.professor (prfs_id, bl_major_id, name, tel) VALUES (7019901, 9901, '김보경', '023445678');
INSERT INTO example.professor (prfs_id, bl_major_id, name, tel) VALUES (7029902, 9902, '조숙', '023446789'); 
INSERT INTO example.professor (prfs_id, bl_major_id, name, tel) VALUES (7039903, 9903, '이호', '023449584'); 
INSERT INTO example.professor (prfs_id, bl_major_id, name, tel) VALUES (7049904, 9904, '박철남', '023449588'); 
INSERT INTO example.professor (prfs_id, bl_major_id, name, tel) VALUES (7059905, 9905, '이만기', '023443443'); 
INSERT INTO example.professor (prfs_id, bl_major_id, name, tel) VALUES (7069901, 9901, '강조교', '023449994'); 
INSERT INTO example.professor (prfs_id, bl_major_id, name, tel) VALUES (7079902, 9902, '이희숙', '023443321'); 
INSERT INTO example.professor (prfs_id, bl_major_id, name, tel) VALUES (7089903, 9903, '소머리', '023440123'); 
INSERT INTO example.professor (prfs_id, bl_major_id, name, tel) VALUES (7099904, 9904, '두수위', '023443327'); 
INSERT INTO example.professor (prfs_id, bl_major_id, name, tel) VALUES (7109905, 9905, '지만래', '023449995'); 
INSERT INTO example.major (major_id, major_title, major_prfs_cnt, major_student_cnt, tel) VALUES (9901, '컴퓨터공학과', 7, 123, '023454321'); 
INSERT INTO example.major (major_id, major_title, major_prfs_cnt, major_student_cnt, tel) VALUES (9902, '아동보육학과', 8, 345, '023456676'); 
INSERT INTO example.major (major_id, major_title, major_prfs_cnt, major_student_cnt, tel) VALUES (9903, '국문학과', 6, 213, '023456567'); 
INSERT INTO example.major (major_id, major_title, major_prfs_cnt, major_student_cnt, tel) VALUES (9904, '경제학과', 5, 432, '023456987'); 
INSERT INTO example.major (major_id, major_title, major_prfs_cnt, major_student_cnt, tel) VALUES (9905, '사회복지학과', 9, 312, '023454534');
```
  
<br/>

__1. JOIN의 개념__  
  
  RDBMS(Relational DataBase Management System, 관계형 데이터베이스 관리 시스템) 에서  
  데이터베이스 내에 있는 테이블이나 스키마들이 서로 관계를 가지고 있는 것을 이용해서 SQL을 작성해야 하는데, 이 때 join이 사용됨.  
  Join을 사용하면 여러 테이블이나 스키마에 분산되어 있는 데이터를 하나의 view 로 출력할 수 있음.  

<br/>

__2. JOIN의 종류__

  (1) 카티션곱 join (Cartesian Product)  
  
  where절이나 on절에 join 조건 없이 테이블들을 join 하는 것.  
  두 테이블의 row 수를 모두 곱한 것만큼의 결과가 출력됨. (모든 데이터를 1:1로 연결)  
  데이터를 많이 불려야 할 때, 연관이 없는 두 테이블의 데이터를 무작위로 합쳐야할 때 등 특정한 조건 안에서 필요한 경우가 있음.  
  
```
SELECT * FROM example.major; //5 rows
SELECT * FROM example.professor; //10 rows
SELECT m.major_id, m.major_title, p.prfs_id, p.name FROM example.major m, example.professor p; //mysql 문법, 5*10 = 50 rows
SELECT m.major_id, m.major_title, p.prfs_id, p.name FROM example.major m cross join example.professor p; //ansi SQL 문법
```

<br/>

  (2) Equi join (inner join, 등가조인)  
  
  가장 보편적인 방법.  
  두 테이블을 연결하는 key가 있을 때 해당 key의 값이 같은 데이터를 (양쪽에 다 존재하는 값만) 결과로 출력.  
    
```
SELECT * FROM example.professor;
SELECT * FROM example.major;
```
  여기서 professor 테이블의 bl_major_id 는 major 테이블의 major_id 와 매핑이 됨.  
  이를 FK(Foreign Key)라고 하며, 두 테이블을 연결하는 key 가 됨.  
  join 시에 조건으로 FK 를 넣어주면 두 테이블을 inner join 할 수 있음.  
  
```
//mysql 문법
SELECT p.name as 교수이름, m.major_title as 학과명
FROM example.professor p, example.major m
WHERE p.bl_major_id = m.major_id;

//ansi SQL 문법 - join, cross join, inner join 모두 같은 결과 출력
SELECT p.name as 교수이름, m.major_title as 학과명
FROM example.professor p join example.major m on p.bl_major_id = m.major_id;

SELECT p.name as 교수이름, m.major_title as 학과명
FROM example.professor p  cross join example.major m on p.bl_major_id = m.major_id;

SELECT p.name as 교수이름, m.major_title as 학과명
FROM example.professor p inner join example.major m on p.bl_major_id = m.major_id;
```

  3개의 테이블을 join 하는 것도 동일함.  
  테이블 1과 테이블 2를 공통의 key 로 연결한 후에, join 한 데이터를 하나의 테이블로 생각하여 테이블 3과 1:1 join 한다.  
  
```
//mysql 문법
SELECT s.name as 학생이름, p.name as 교수이름, m.major_title as 학과명
FROM example.student s, example.major m, example.professor p
WHERE s.bl_prfs_id = p.prfs_id and p.bl_major_id = m.major_id;

//ansi SQL 문법
SELECT s.name as 학생이름, p.name as 교수이름, m.major_title as 학과명
FROM example.student s
    inner join example.major m
    inner join example.professor p
        on s.bl_prfs_id = p.prfs_id
          and p.bl_major_id = m.major_id;
```

<br/>

  (3) Non-equi join (비등가 join)  
  
  Equi join과 반대 개념. 두 테이블을 join 할 때, 값이 서로 같지는 않지만 join 조건에서 지정한 어느 범위에 일치할 때 데이터를 join.  
  즉, '=' 연산자가 아닌 다른 조건으로 join 을 수행하는 방법.  

```
CREATE TABLE example.customer (name varchar(10), point int);
CREATE TABLE example.gift (name varchar(20) null, point_s int null, point_e int null);
INSERT INTO example.customer (name, point) VALUES ('조성모', 5);
INSERT INTO example.customer (name, point) VALUES ('이기찬', 12);
INSERT INTO example.customer (name, point) VALUES ('이소라', 14);
INSERT INTO example.customer (name, point) VALUES ('서태지', 18);
INSERT INTO example.customer (name, point) VALUES ('박효신', 21);
INSERT INTO example.customer (name, point) VALUES ('김정민', 16);
INSERT INTO example.customer (name, point) VALUES ('양파', 9);
INSERT INTO example.customer (name, point) VALUES ('강수지', 22);
INSERT INTO example.customer (name, point) VALUES ('강타', 24);
INSERT INTO example.gift (name, point_s, point_e) VALUES ('공기청정기', 11, 15);
INSERT INTO example.gift (name, point_s, point_e) VALUES ('아이폰', 21, 25);
INSERT INTO example.gift (name, point_s, point_e) VALUES ('로봇청소기', 6, 10);
INSERT INTO example.gift (name, point_s, point_e) VALUES ('상품권', 1, 5);
INSERT INTO example.gift (name, point_s, point_e) VALUES ('스마트패드', 16, 20);
SELECT * FROM example.customer;
SELECT * FROM example.gift;
```

```
//mysql 문법
SELECT c.name as 고객명, c.point as 고객_point, g.name as 상품명
FROM example.customer c, example.gift g
WHERE c.point between g.point_s and g.point_e; 
//gift 테이블의 point_s와 point_e 사이에 customer 테이블의 값이 해당된다면 두 테이블을 join 하라.

//ansi SQL 
SELECT c.name as 고객명, c.point as 고객_point, g.name as 상품명
FROM example.customer c join example.gift g
on c.point between g.point_s and g.point_e;
```

<br/>

  (4) Outer join  
  
  inner join 은 양쪽 테이블에 모두 존재하는 데이터만 출력하지만, outer join 은 한쪽을 기준으로 하여 다른 쪽에 key값이 일치하는 것이 없더라도 모두 출력.  
  left outer join, right outer join, full outer join 으로 구분됨.(mysql에서는 full outer join 지원하지 않아 union으로 우회적 사용)  
  left outer join 과 right outer join 은 왼쪽과 오른쪽 중 어디에 기준을 둘 것이냐에 따라 다름.  
  
  ![image](https://user-images.githubusercontent.com/73428030/133917860-95632e70-1a97-4d0f-98fd-b13d50b91dea.png)  
  
  outer join 은 모든 데이터를 가지고 올 때 full scan을 하므로 DB에 무리가 될 수 있어 필요할 때만 사용해야 함.  
  
```
//데이터 추가
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1031, 9901, null, '신채령', '01044755564'); 
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1032, 9902, null, '이만도', '01022287777'); 
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1033, 9903, null, '박만호', '01099972253'); 
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1034, 9904, null, '최이강', '01029386577'); 
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1035, 9905, null, '강이민', '01033334444'); 
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1036, 9901, null, '민형도', '01099973331'); 
INSERT INTO example.student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1037, 9902, null, '도지란', '01055567774');
SELECT * FROM example.student;
SELECT * FROM example.professor;
```
  
  위에서 추가한 데이터로 인해, 담당 교수 ID가 없는 학생들이 일부 존재하게 됨.  
  이때, student 테이블과 professor 테이블을 일반 inner join으로 join한다면 전체 학생 중에서 담당 교수가 배정되지 않은 학생들이 제외됨.  
  이러한 누락없이 모든 학생들의 데이터를 나타내고자 할 때 outer join 을 사용.  
  left outer join (student 테이블을 left 테이블이라 할 경우) 을 하면 bl_prfs_id 에 값이 없거나 professor 테이블과 연결이 되지 않은 데이터들은 null로 출력됨.  
  mysql은 outer join을 ANSI SQL 형태로 작성해야 함.  
  
```
//Left outer join
SELECT s.name, s.bl_prfs_id, p.name, p.prfs_id
FROM example.student s 
	left outer join example.professor p
		on s.bl_prfs_id = p.prfs_id;
    
//Right outer join
SELECT s.name, s.bl_prfs_id, p.name, p.prfs_id
FROM example.student s
	right outer join example.professor p
		on s.bl_prfs_id = p.prfs_id;
```

<br/>

  (5) Self join  
  
  한 테이블이 자기자신과 join 하는 경우.  


