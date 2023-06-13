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
 #  
 #  
 ### 순수 JDBC와 DB 연결
  - <img width="663" alt="스크린샷 2023-06-12 오후 10 50 28" src="https://github.com/pnci1029/TIL/assets/81909140/a1e80bd1-26c8-41e7-9d1c-2b1acd833499">
  ```
    JDBC는 자바 표준 Connection(java.sql.connection)(인터페이스)을 구현
    H2 데이터베이스 드라이버는 JDBC Connection 인터페이스를 구현한 org.h2.jdbc.jdbcConnection을 제공
    
  ```
  - DriverManager 커넥션 흐름
  - <img width="645" alt="스크린샷 2023-06-12 오후 10 54 54" src="https://github.com/pnci1029/TIL/assets/81909140/c6db327d-9670-4601-baa5-bf85d1caa658">
  ```
     1. DB커넥션이 필요한 경우 자바에서 제공하는 DriverManager.getConnection(); 호출
     2. DriverManager에서 라이브러리에 등록된 데이터베이스 자동 연결. 커넥션을 얻을 수 있는지 확인 후 DB 커넥션 제공
      (인터페이스 : 자바 SQL Connection 구현체: 해당 DB 드라이버 구현체)
     3. 이렇게 제공된 커넥션 구현체가 클라이언트에 반환
  ```
#  
#  
### ResultSet
  ```
    try {
          connection = getConnection();
          preparedStatement = connection.prepareStatement(sql);
          preparedStatement.setString(1, memberId);

          rs = preparedStatement.executeQuery(); // ResultSet
          if (rs.next()) {
              Member member = new Member();
              member.setMemberId(rs.getString("member_id"));
              member.setMoney(rs.getInt("money"));
              return member;
          } else {
              throw new NoSuchElementException();
          }

      } catch (SQLException e) {
          log.error("error", e);
          throw e;
      } finally {
          close(connection, preparedStatement, rs);
      }
  ```
  - <img width="657" alt="스크린샷 2023-06-13 오후 10 16 49" src="https://github.com/pnci1029/TIL/assets/81909140/986994a7-f64f-41b9-b458-1602a3dd6436">
  - 다음과 같이 생긴 자료구조
    - ex) select member_id, member_name ~ 쿼리를 실행하면 `member_id`, `member_name`으로 resultSet에 저장됨
  - resultSet 내부의 커서로 다음 데이터를 조회 (rs.next())
  - 최초 한번이상 커서 이동을 해야 조회가 가능함
    - rs.next()는 boolean을 반환타입으로 가지며, true이면 데이터가 있고, false 반환시 데이터가 없다는 의미


 

