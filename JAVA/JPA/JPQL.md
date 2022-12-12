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
        navite1; + navite2;
        
        -> 해당 쿼리 결과 "select m from member mwhere m.name like "%Kim%""
        -> String 값을 더하는 과정에서 에러 발생요소 생성
        -> 동적쿼리에 적합하지 않다.
      }
  - 단 적절한 시기에 영속성 컨텍스트에 있는 객체들을 db로 flush 필요
  
  
  ```
