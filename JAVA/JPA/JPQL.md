*. JPQL?
  - 
  - JPA에서 사용하는 표준문법 - QueryDSL, JPA Criteria  ->  (자바 코드로 JPQL을 빌드해주는 제네레이터 클래스 모음)
  - JPQL을 사용하더라도 DB에 좀 더 종속적인 쿼리 사용이 필요할 때 -> 네이티브 쿼리 / MyBatis / SpringJDBCTemplates 사용
  - 
  ```
  JPQL vs 네이티브 쿼리?

  컴파일에러 vs 런타임에러
  동적쿼리 사용 시 JPQL 사용이 유리
   -> 네이티브쿼리로 동적쿼리 사용 시 String + String
      ex)
      String native1 = "select m from member m"
      if(member.getName() != null){
        String navite2 = "where m.name like "%Kim%"";
        return (navite1 + navite2);
        
        -> 해당 쿼리 결과 "select m from member mwhere m.name like "%Kim%""
        -> String 값을 더하는 과정에서 에러 발생요소 생성
        -> 동적쿼리에 적합하지 않다.
      }
  ```
  - 단 적절한 시기에 영속성 컨텍스트에 있는 객체들을 db로 flush 필요  
  #  
*. JPQL 사용
  - 
  - 반환타입 
  ```
  em.createQuery("select m from Member m", Member.class);   -> 멤버 객체 반환 
  em.createQuery("select m.userName from Member m", String.class);   -> 문자열 객체반환 
  -> 반환 타입이 명확할때 TypeQuery 사용
  ->TypeQuery<Member> query = em.createQuery("select m.userName from Member m", String.class);
  
  em.createQuery("select m.userName, m.age from Member m"); -> 반환타입이 불분명함
  -> 반환타입이 명확하지 않을 때 Query 사용
  -> Query query = em.createQuery("select m.userName, m.age from Member m");
  ```  
  #  
  - 결과 조회
    - 결과가 자바 컬렉션일때(결과가 하나 이상일 때) & 결과가 없을 시 빈 리스트 반환(Exception 발생 X)
      - query.getResultList();
    - 결과가 정확히 하나일 때(단일 객체 반환)
      - query.getSingleResult();
      - 결과가 없을 시 NoResultException
      - 결과가 둘 이상일 시 NonUniqueResultExceptino  
      #  
      #  
      #  
  - 파라미터 바인딩 




