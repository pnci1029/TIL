## DataModeling
  - 추상화(실체하는 데이터를 데이터페이스로 표현하기 위한 추상화)
  - 단순화(복잡한 문제를 피하여 누구나 이해할 수 있도록 표현)
  - 명확성(위미가 모호하지않고 명확하게 해석되어야함)
#  
#### 데이터 모델링의 단계
  ```
    1. 개념적 모델링
      - 추상화 수준이 가장 높은 모델링단계
      - 엔티티와 속성을 도출하고 ERD를 작성
       * 엔티티 : 사람, 장소, 물건등 업무상 관리가 필요한 관심사를 명사로 지칭한 것

    2. 논리적 모델링
      - 개념적으로 도출한 모델링을 논리적으로 변환하는 작업
      - 테이블간의 관계와 같은 논리성 정의
      - 정규화를 통해 데이터 모델의 독립성 확보
      - 테이블의 무결성 유지

    3. 물리적 모델링
      - 성능, 보안, 가용성을 고려하여 구축
      - 실제 데이터베이스 구축(테이블, 인덱스, 함수 생성)
      - 로컬이나 실제 서버를 만드는 과정
  ```
#  
#### ERD
  - 데이터 모델링의 표준으로 사용되고 있음
  - 소프트웨어 개념으로 이해
  - 개념적 모델링 도출 후 논리적 모델링 과정에서 작성
  ```
    ERD 작성 절차

    1. 엔티티 도출과 엔티티 작성

    2. 엔티티 배치
      - 중요한 엔티티는 왼쪽 상단에 배치하는게 일반적

    3. 배치된 엔티티 간 관계 설정

    4. 엔티티 관계 서술

    5. 엔티티 참여도 표현

    6. 테이블 관계의 필수 여부 표현(FK, PK)
  ```
