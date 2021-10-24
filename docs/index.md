Index
=============

__1. Full scan & Range scan__

  Full scan: 테이블에 포함된 레코드를 처음부터 끝까지 엑세스  
  Range scan: 테이블의 일부 레코드에만 엑세스  
  
  실행하고자 하는 쿼리 앞에 explain 을 붙여주면 full/range scan 여부를 확인할 수 있다.  
    
```
explain SELECT * FROM example.user; //type = ALL (full scan)
explain SELECT * FROM example.user WHERE idx between 1 and 10; //type = range (range scan)
```

<br/>

__2. Index 란__

  데이터를 찾을 때 range scan 을 할 수 있도록 해주는 색인 개념.  
  테이블에 대한 동작 속도를 높여준다.(특히 검색)  
  인덱스는 테이블 내의 1개 또는 여러개의 칼럼으로 생성할 수 있다.  
   
<br/>
    
__3. Index 를 만드는 기준__

  (1) 데이터가 많은 테이블에 권장  
  
  테이블 내 데이터가 많지 않은 경우에는 full scan 이 index scan 보다 빠를 수 있다.  
  인덱스는 데이터가 많을수록 더 효과가 크다.  
  
  (2) primary key 나 unique 제약이 부여된 열에는 불필요  
  
  PK나 유일성 제약이 부여된 칼럼에는 자동으로 인덱스(클러스터 인덱스)가 생성되어 따로 추가할 필요 없음.  
  이 두가지 경우에는 값의 중복 체크를 위해 데이터를 정렬하는 과정에서 암묵적으로 인덱스가 사용되기 때문임.  
  
  (3) Cardinality가 높은 열  
  
  Cardinality = 값의 분산도  
  특정 칼럼에 대해 많은 종류의 값을 가지면, cardinality 가 높다. (eg. 주민등록번호)  
  특정 칼럼에 대해 적은 종류의 값을 가지면, cardinality 가 낮다. (eg. 성별)  
  cardinality 가 낮은 경우 인덱스 트리를 따라가는데 조작이 증가하여 오버헤드 증가로 인덱스의 효과가 떨어짐.  
  
  (4) WHERE, ORDER BY, SELECT절에 자주 등장하는 칼럼 or JOIN 이 자주 사용되는 열  
  
  <br/>

__4. Index 의 역효과__

  (1) 오버헤드  
  
  테이블에 데이터가 INSERT, UPDATE, DELETE 될때마다 인덱스를 갱신하는 것.  
  SELECT가 빨라지지만, 그만큼 INSERT, UPDATE, DELETE 작업은 느려질 수 있음.  
  따라서 데이터 변경작업이 잦을 경우 오히려 성능이 약화될 가능성이 있음.  
  
  (2) 오사용  
  
  하나의 테이블에 다수의 인덱스를 생성할 경우 옵티마이저가 실행계획을 만들 때 의도하지 않은 인덱스를 사용할 수 있음.  
  
  (3) 기타 단점들  
  - 인덱스가 데이터베이스 공간을 차지 (10% 정도의 추가 공간 필요)  
  - 초기 인덱스 생성 시 시간이 많이 소요  
  - SELECT는 빨라지지만 INSERT나 UPDATE는 느려짐  

<br/>

__5. Index 의 종류__

  (1) 클러스터 인덱스  
  
  primary key 설정시 자동생성됨. PK 칼럼 데이터가 변경되어도 항상 정렬을 유지.  
  테이블 당 1개의 클러스터 인덱스를 생성할 수 있음.  
  지정된 칼럼을 기준으로 데이터가 물리적으로 정렬되므로 추가적인 공간이 필요하지 않음.  
  SELECT 는 빠르지만, INSERT, UPDATE, DELETE는 정렬 작업으로 인해 성능이 떨어지게 됨.  
  
  (2) 단일 인덱스  
  
  인덱스 생성 시 하나의 칼럼만 지정하는 경우.  
  데이터가 많지 않은 경우에 주로 사용.  
  
  (3) 복합 인덱스  
  
  인덱스 생성 시 두 개 이상의 칼럼을 지정하는 경우.  
  
  (4) 커버드 인덱스  
  
  출력하는 칼럼과 조건에 삽입된 칼럼이 모두 인덱스에 정보가 있어서 실제 테이블을 조회하지 않고도 데이터를 가지고 올 수 있는 경우.  
  
  (5) B-Tree 인덱스  
  
  가장 많이 사용하는 인덱스. 데이터가 정렬된 상태로 유지되어 있음.  
  3개의 노드로 구분됨.  
  
  |Node명|설명|
  |---|---|
  |Root node|최상위 노드|
  |Leaf node|최하위 노드|
  |Branch node|Root와 leaf를 연결하는 노드|
  
  B-tree는 어떤 값에 대해서도 같은 시간에 결과를 얻을 수 있다. O(logN)  
  B+tree라는 개념도 있음. (추후 업데이트)  
  
  <br/>

__6. Index 사용예제__

```
//인덱스 생성
CREATE INDEX idx_test on example.user (email); //OR
ALTER TABLE example.user ADD INDEX idx_test (email); //단일 인덱스
ALTER TABLE example.user ADD INDEX idx_test (email, company); //복합 인덱스

//인덱스 삭제
ALTER TABLE example.user DROP INDEX idx_test;

//유니크 인덱스 생성
ALTER TABLE example.user ADD UNIQUE INDEX idx_test (email, company);

//생성된 인덱스 확인
SHOW INDEX FROM example.user;
```
