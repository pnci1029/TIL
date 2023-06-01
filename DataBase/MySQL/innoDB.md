# INNODB이란?
  - ![쿼리](https://github.com/pnci1029/TIL/assets/81909140/64732701-3ea5-474a-bf3d-1f1b9195f5cb)
  ```
  MySQL에서 사용하는 스토리지 엔진(데이터베이스 엔진)

  * 스토리지엔진
    - DBMS에서 데이터를 CRUD 처리를 위해 사용하는 기본적인 컴포넌트
    - 실제 데이터를 디스크 스토리지에 저장하거나 불러오는 기능 처리
    - 플러그인 방식으로 사용가능하여 원하는 스토리지엔진 사용
    - show engines 명령어를 통해 확인 가능
    - MySQL 엔진과 달리 스토리지엔진은 동시에 여러개 사용 가능
    
  ```
  #  
  - <img width="788" alt="스크린샷 2023-06-01 오후 8 46 48" src="https://github.com/pnci1029/TIL/assets/81909140/cc3e989f-a740-4017-9d1f-973313628c15">
  ```
  1. Buffer Pool 존재(Oracle의 Buffer Cache와 유사)
    - 디스크상의 데이터 파일이나 인덱스 정보를 캐싱하기 위한 공간
    
  2. PK를 기반으로 쿼리를 최적화하도록 디스크에 정렬하여 저장
  
  3. MVCC를 이용하여 멀티 유저에게 동시성 제공
    - Multi Version Concurrency Control
    - 하나의 레코드에 대해 여러버전을 관리하는 방식
    - 세션별로 해당 데이터를 조회하거나 작성시 정합성을 보장하는 메커니즘
  
  4. 커밋, 롤백등 복구기능을 가진 트랜잭션 지원
  
  5. ACID (원자성, 일관성, 격리성, 내구성) 모델을 따르며 트랜잭션의 유효성을 보장
  
  6. Undo Log
    - 롤백과 동시성 제어를 위해 사용
    - 데이터가 수정이나 삭제되었을 때 변경 이전 상태를 보관
      1. update쿼리 실행 시 실제 데이터에 변경된 데이터가 저장.
      2. Undo Log에는 변경 이전의 데이터 백업
      3. Commit 시 변경된 데이터 사용
      4. RollBack 시 Undo 영역의 변경이전 데이터로 복구
  
  
  ```
  #  
  #  
  #  
  referred by (https://blog.ex-em.com/1680, https://neocan.tistory.com/396, https://velog.io/@inhwa1025/MySQL-InnoDB%EB%9E%80, https://unordinarydays.tistory.com/159)
