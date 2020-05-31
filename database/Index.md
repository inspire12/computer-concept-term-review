# Index


### 개요
+ 인덱스는 특정 칼럼 값을 가지고 있는 열을 빠르게 찾기 위해 사용한다.
  - ex) 책에서 목차 -> 책의 목차를 보고 원하는 페이지를 바로 찾아간다.
+ 칼럼에 대한 인덱스(목차)를 가지고 있다면 모든 데이터를 조사하지 않고도 인덱스를 보고 검색 위치를 빠르게 찾는다.

+ **장점**
  - 검색 속도의 향상
  - 해당 쿼리의 부하가 줄어, 시스템 전체의 성능 향상
+ **단점**
  - 추가 공간이 필요하다. (데이터베이스의 약 10%)
  - 처음 인덱스를 생성하는 시간이 많이 소요될 수 있다.
  - 데이터의 변경이 자주 일어나면 오히려 성능이 나빠질 수 있다.
  
  
---
### B-Tree (Balanced Tree)
#### 페이지
  + 최소한의 저장 단위 (16KB)
  + 데이터 1개만 저장해도 1개의 페이지를 차지
  + 모든 데이터가 정렬
  + 전체 테이블 검색 보다 빠른 탐색
  
<img src="https://github.com/ISKU/computer-concept-term-review/blob/docs/database/Database/img/IMG_01.png" width="400">


#### 페이지 분할
  - 데이터의 변경 작업시 성능이 나빠지는 단점
    - INSERT, UPDATE, DELETE

<img src="https://github.com/ISKU/computer-concept-term-review/blob/docs/database/Database/img/IMG_02.png" width="400">
<img src="https://github.com/ISKU/computer-concept-term-review/blob/docs/database/Database/img/IMG_03.png" width="400">


---
### 종류
+ 클러스터형 인덱스
  - 사전 순서로 정렬되어 있다.
    - ex) 영어사전, 인덱스 자체가 책의 내용과 같은 것
  - 테이블당 한 개만 생성
+ 보조 인덱스
  - ex) 목차, 별도로 인덱스를 구성
  - 테이블당 여러 개 생성 가능
  
  
#### 클러스터형 인덱스
+ 테이블당 1개만 생성
+ Primary Key 지정시 자동생성
  - 테이블에 기본키는 1개만 가능
    - 즉, 클러스터형 인덱스도 1개만 자동으로 생성
+ Primary Key
+ Unique Not NULL
+ 구조
<img src="https://github.com/ISKU/computer-concept-term-review/blob/docs/database/Database/img/IMG_04.png" width="800">



#### 보조 인덱스
+ 구조
<img src="https://github.com/ISKU/computer-concept-term-review/blob/docs/database/Database/img/IMG_05.png" width="800">

---
### 인덱스 실행 비교

+ 인덱스가 없는 쿼리 실행
  - Full Table Scan
+ 인덱스 생성 후 쿼리 실행
  - 인덱스의 사용으로 cost 감소

<img src="https://github.com/ISKU/computer-concept-term-review/blob/docs/database/Database/img/IMG_06.png" width="500">

  
---
### 인덱스의 사용
+ 인덱스는 열 단위에 생성된다
  - Where 절에서 사용되는 열에 인덱스를 만들어야 한다.
+ Where 절에서 사용되더라도 자주 사용해야 하는 경우
  - SELECT보다 INSERT의 비율이 더 높다면?
+ 데이터의: 중복도가 높은 열은 인덱스를 만들어도 별 효과가 없다.
  - 크게 성능 향상의 효과가 없는 경우 발생
  - 인덱스 관리에 대한 비용 때문에 없는게 나을 수도 있다.
+ 외래키를 지정한 열에는 자동으로 외래키 인덱스가 생성
+ Join에 자주 사용되는 열에는 인덱스를 생성하는 것이 좋다.
+ INSERT, UPDATE, DELETE가 얼마나 자주 일어나는지 고려
  - 인덱스는 조회시에만 성능을 향상 시킨다.
  - 데이터의 변경에서는 오히려 부담을 주게 된다.
+ 클러스터형 인덱스는 테이블당 하나만 생성 (없을 수도 있다)
+ 사용하지 않는 인덱스는 제거
  - 공간 확보
  - 데이터 입력시 발생되는 부하를 줄인다.
