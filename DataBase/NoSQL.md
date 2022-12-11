*. Redis Cache vs Memcached
  - 
  - 공통점
  ```
  Key - Value 형식의 NoSQL
  RDB의 서브 역할로 많이 사용
  인메모리 데이터베이스
  ```
  - 
  - 차이점
  ```
  Redis                                         Memcached
   - 컬렉션(자료구조)                            - 문자열(String)
   - 인메모리 + 디스크 저장                      - 메모리만 저장
      (메모리 유실 시 데이터 복)
   - 싱글스레드                                 - 멀티스레드
      (백만 건의 데이터 삭제 요청 시 큰 속도차이 발생)
   - Master - Slave 구조로 여러 복제본(Slave) 생성가능 (높은 가용성 - 오랫동안 고장 없이 사용)
```
- Master - Slave 구조란?
  - 문제상황   -    하나의 데이터베이스에 너무 많은 쿼리 요청 발생 -> 원본 DB(Master)의 과부하를 막고자 Slave DB에서 원본 DB 대신 응답
  - 주로 읽기 처리를 할 때 Slave DB
    - Master DB와 Slave DB의 동기화 방법? 
      1. 처음에 들어온 정보들을 Master DB에 반영 
      2. 반영된 변경 이력들을 Binary Log에 저장
      3. Slave DB에서 최신 데이터 요청
      4. Master DB는 Binary Log를 Slave DB에 전달
      5. Slave DB는 Binary Log를 읽고 Relay Log에 저장
      6. Relay Log를 읽고 Slave DB에 저장
