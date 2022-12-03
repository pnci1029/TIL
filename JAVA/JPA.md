*. JPA 동작 순서?
  - 
  - JVM 안에서 전체 동작
  1. 자바 객체(Entity)를 RDB에 접근하도록 JPA를 사용하여 요청
  2. JPA에서 Entity 분석
  3. Insert / Select / Delete 등 SQL 생성
  4. JDBC Api 사용
  5. 패러다임 불일치성 해소
  6. 


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


*. JPA 사용 이유?
  -
  - ORM을 통한 객체와 RDB 매핑 
  - SQL dialect 제공
  - 동일한 트랜잭션내 엔티티의 동일성 보장
    ```
    String memberId = "100";
    Member member1 = jpa.find(Member.class, memberId)  -> SQL을 통한 조회
    Member member2 = jpa.find(Member.class, memberId)  -> 캐싱된 메모리에서 조회 (성능 향)
    
    member1 == member2
    ```
  - JPA vs JDBC

*. 지연로딩        vs      즉시로딩?
  - 
  - 즉시로딩 -> DB 접근 SQl 요청 시 연관관계 매핑된 모든 테이블 데이터 조회
  - 지연로딩 -> SQL 요청 시 테이블 조회가 필요한 DB만 접
  ```
  지연로딩  member.getMember(memberId)     -> Select * FROM Member
            member.getTeam(memberid)       -> Select * FROM Member
                                           -> Select * FROM Member

  즉시로딩  member.getMember(memberId)     -> Select * FROM Member
                                           -> Select * FROM Member
            member.getTeam(memberid)       -> Select * FROM Member
                                           -> Select * FROM Member
  ```
    
    
*. 영속성 컨텍스?
  - 
  - 엔티티를 영구 저장하는 환경
  - 한 트랜잭션 내에서 짧은기간동안 수행 후 비즈니스 로직 종료 후에 지워짐 
  - 엔티티와 db 사이에 존재
    - 1차 캐시 (아래 상태로 보관)
    ```
    key(@id)             value(Entity)
    memberId(pk)         Member(객체)
    
    Member객체 조회시
    -> 1. 영속성 컨텍스트 캐시에 객체 존재여부 확인
    -> 2. 존재 시 결과값 반환(db접근X) -> 속도 향상
    -> 3. 캐시에 없을 시 db에 접근
    -> 4. 1차 캐시에 해당 객체 등록 후 결과값 
    ```
  - 변경감지(dirtyChecking / 엔티티수정)
  ```
  Member member = new Member(1L, "JPA"); // 비영속상태
  em.persist(member); // 영속화
  em.commit(); // db에 저장(jpa에서 쿼리 작성)
  
  member.setName("JAVA"); // 기존 멤버객체값 수정
  em.persist(member) -> 불필요
  )))자바 컬렉션 사용 시 수정 후 다시 저장하지 않음 으로 이해
  ```
  - 


*. 엔티티 생명주기?
  - 
  1. 비영속 상태
    ```
    Member member = new Member();
    member.setId(1L);
    member.setName("JPA");
    ```
  2. 영속상태
        ```
    Member member = new Member();
    member.setId(1L);
    member.setName("JPA");
    +
    EntityManager em = emf.createdEntityManager();
    em.getTransaction.began();
    
    em.persiste(member);
    
    -> 영속성 컨텍스트 내 member객체 등록 
    ```
         
