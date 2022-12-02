*. JPA 동작 순서?
  - 
  - JVM 안에서 전체 동작
  1. 자바 객체(Entity)를 RDB에 접근하도록 JPA를 사용하여 요청
  2. JPA에서 Entity 분석
  3. Insert / Select / Delete 등 SQL 생성
  4. JDBC Api 사용
  5. 패러다임 불일치성 해


*. 객체와 RDB 차이
  - 
  - 상속  
  #
          객체                  관계형 DB
    - 객체간의 상속 가능 <-> 슈퍼타입 서브타입 관계 테이블 (PK, FK...)
    - 
  - 연관관계
  - 데이터타입
  - 데이터 식별방법


*. ORM?
  - 
  - Object-Relational Mapping
  - ORM 프레임워크는 객체 <-> RDB 를 각각 개발했을 때 가운데에서 객체와 관계형DB를 매핑 역할을 해주는 기술
  - 
