# JDBC
  - <img width="818" alt="스크린샷 2023-06-07 오후 9 47 38" src="https://github.com/pnci1029/TIL/assets/81909140/4ff5324f-7293-4430-bf02-1ccb71c09710">
  ```
    자바에서 데이터베이스에 접근할수있도록 사용하는 자바 API
    
    java.sql.Connection   연결
    java.sql.Statement    SQL을 담은 내용
    java.sql.ResultSet    SQL 요청 응답
    등 대표 3가지 기능을 표준 인터페이스로 정의하여 제공
    
    개발자는 JDBC 인터페이스를 개발하여 사용
    
    ex) java - mysql
        => MYSQL JDBC DRIVER
  ```
  - <img width="576" alt="스크린샷 2023-06-07 오후 9 51 46" src="https://github.com/pnci1029/TIL/assets/81909140/92b10e4f-804c-4d14-971c-64a8ab78e4bb">
  ```
  1. 데이터베이스 종류에 따라 사용해야하는 코드 변경 문제 해결
      => 추상화에 의존
      
  2. DB 연결, 전달, 응답 학습 내용을 인터페이스 구현을 통해 해결
  ```
#  
#  
## 순수 JDBC와 SQL MAPPER
  - <img width="679" alt="스크린샷 2023-06-07 오후 9 58 21" src="https://github.com/pnci1029/TIL/assets/81909140/0cb35253-30aa-454b-85a2-6ae3425f1363">
  ```
  SQL MAPPER
    - SQL 응답결과를 객체로 반환
    - JDBC 반복코드 제거
    - 개발자가 직접 SQL 작성
    
  JDBC Template, MyBatis
  ```
  
#  
#  
## ORM
  - <img width="681" alt="스크린샷 2023-06-07 오후 10 01 52" src="https://github.com/pnci1029/TIL/assets/81909140/fbc6ca48-90b6-4bde-a668-b53a8588a1e2">
  ```
    - 객체를 관계형 DB와 매핑시켜주는 기술
    - 개발자가 직접 SQL을 작성하지 않고 DB에 접근
    
    JPA, Hibernate, 이클립스 링크
    * JPA는 자바진영의 표준 ORM 인터페이스이고, 이것을 구현한 하이버네이트와 이클립스 링크가 있다.
  ```
#  
#  
### SQL MAPPER vs ORM
  ```
  SQL MAPPER
    - SQL 작성 요령을 알면 나머지는 Sql Mapper가 해결. SQL 작성이 가능하면 금방 습득 가능
    
  ORM
    - 직접 SQL 작성이 없이 DB 접근이 가능하여 생산성이 높아짐
    - 높은 이해도 필요
    
    
    * Sql Mapper, ORM 모두 내부적으로 JDBC 사용
    
  ```

