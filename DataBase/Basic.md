*. DB Connection?
  - 
  - 데이터베이스를 사용하기 위해 DB와 어플리케이션 간 통신을 도와주는 수단 
  - DB Driver와 연결정보를 담은 URL 요구 
  - JAVA의 DB Connection은 JDBC의 URL 타입 사용 
    - ![dbconnection](https://user-images.githubusercontent.com/81909140/206901738-c4e955e6-d534-44dc-8de9-0278c821f087.png)  
#
    
*. Connection Pool(DBCP)?
  - 
  - DB Connection을 직접 하는 경우 클라이언트의 요청 마다 JDBC 드라이버 로드 + 커넥션 객체 생성 해야함 -> 매우  비효율적
  - DB Connection의 효율성 문제 해결을 위해 사용
  ```
  MySQL 기준 Insert 문 수행 시 필요 비용
  1. Connecting (3) 
  2. Sending query to server (2)
  3. Parsing query (2)
  4. Inserting row (1)
  5. Inserting index(1)
  6. Closing (1)
  
  -> 연결 시 발생하 비용이 가장 큼
  -> Connection Pool을 통해 보완
  ```
  - 동작원리
    1. WAS가 실행되면 일정량의 Connection 객체를 미리 생성 후 pool에 저장
    2. 클라이언트 요청 발생 시 생성된 Connection 객체 할당
    3. 요청 완료 시 다시 Connection 객체 반납 후 Pool에 저장
    - ![connectionpool](https://user-images.githubusercontent.com/81909140/206902005-056ed723-a614-46a0-b644-fa736769be6b.png)  
# 

*. 커넥션 풀은 무조건 클 수록 좋을까?
  - 
  - 커넥션 풀을 크게 설정 시  -> 커넥션 풀이 스레드보다 크다면 남는 커넥션 풀 발생으로 메모리 낭비 발생
  - 커넥션 풀을 작게 설정 시  -> HandOffQueue에 다수의 스레드 대기  -> 30초 대기시간 초과로 인한 Exception 발생 
    - 풀 사이즈 = 스레드 개수*(하나의 트랜젝션 내 필요한 커넥션 수 -1)+1 권장  
#

*. HikariCP?
  - 
  - JDBC Connection Pool 프레임워크
  - 커넥션 풀 관리를 위해 Hikari CP 사용 
  - 동작방식
    1.  스레드 -> HikariCP에 Connection 객체 요청
    2. 이전에 사용했던 Connection 있는지 확인
    3.  존재 시 다른 스레드가 사용중일 경우 전체 Connection 조회(Loop)
        -   커넥션이 존재하지 않는다면 HandOffQueue를 돌며 다른 스레드가 Connection 반납하길 기다린다.
          -  30초(디폴트) 동안 반납되는 Connection이 없을경우 예외 발생
          -   ![커넥션풀에러](https://user-images.githubusercontent.com/81909140/206903290-bc284187-26a7-4c53-aa27-cd92fcbfa390.png)
        - 커넥션이 존재한다면 다른 스레드가 반납한 Connection 객체를 받음
    4.  해당 스레드가 Connection 사용 후 다시 반납
    5.  해당 스레드가 해당 Connection 사용 정보 기
  - ![커넥션풀동작](https://user-images.githubusercontent.com/81909140/206903475-689fb537-2a61-439d-a51d-82983da15e19.png)








출처(https://techblog.woowahan.com/2664/)
