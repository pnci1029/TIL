*. Q. Member객체와 Team 객체가 연관관계가 맺어져 있을 때, Member객체 컬럼을 조회했을 때 Team 객체까지 조회를 해야할까?
  
  #
  #

*. em.find() vs em.getReference()
  - 
  - em.find() -> db를 통해 실제 엔티티 엔티티 객체 조회
    -> db에 쿼리 요청을 통해 데이터 조회
  - em.getReference() -> db 조회를 미루는 가짜(proxy) 엔티티 객체 조회
    -> db에 쿼리 요청이 없는데 데이터가 조회됨  
    #  
    #
    
*. 프록시 객체 특징?
  - 
  - 실제 엔티티를 상속받아 프록시 객체가 생성됨 (겉모양이 같다.)
  - 사용하는 입장에서는 실제 엔티티객체인지 프록시 객체인지 구분하지않고 사용하면됨
  - ![proxy](https://user-images.githubusercontent.com/81909140/205571781-673bad77-af0d-4a6c-81e6-8a05bc6f7e77.png)
   - 초기화 진행순서
     1. 멤버객체의 name값 호출 위해 getName 요청
     2. 초기에 프록시 객체(Member target)에는 name 값이 없기 때문에 영속성 컨텍스트에 요청
     3. JPA -> db에 요청 
     4. 실제 Member 엔티티 객체 생성
     5. Member target <-> 실제 객체 연결 
     6. target에 실제 getName 등록
     7. 반환 

