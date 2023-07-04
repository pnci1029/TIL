  ```
  스키마란?

    데이터베이스에서 소유하고 있는 테이블이나 인덱스, 객체 등 논리적 컨테이너들을
    통체적으로 관리하는 계
  ```
## 3층 스키마
  - 사용자, 설계자, 개발자 (3층)가 DB를 보는 관점에 따라 DB를 기술하고, 이들간의 관계를 정의한 ANSI 표준
  - DB의 독립성을 확보하기 위한 방법
  - 3단계 계층의 각 계층을 뷰라고 한다. 일종의 가상 테이블로 이해
  - 3층 스키마 구조
  - <img width="495" alt="스크린샷 2023-07-04 오후 10 22 09" src="https://github.com/pnci1029/TIL/assets/81909140/19dc881e-e929-47b5-995a-8b43751bfa8f">
  ```
    3층 스키마의 구조

    1. 외부 스키마
      - 사용자 관점, 업무상 관련이 있는 데이터 접근
      - 직원들이 직접 접근하는 스키마
      - 뷰를 표시(데이터베이스에 직접 접근X)
      - 응용 프로그램이 접근하는 데이터베이스를 정의

    2. 개념 스키마
      - 설계자 관점
      - 통합 데이터베이스 구조
      - 전체 데이터베이스 내의 규칙과 구조를 표현

    3. 내부 스키마
      - 개발자 관점
      - 데이터베이스의 물리적 저장 구조
      - 데이터 저장 구조, 레코드 구조, 필드 정의 등 포함
  ```