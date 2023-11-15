# 데이터베이스
```
  데이터의 집합체를 관리 운영하는 역할

  여러명의 사용자가 동시 접근이 가능해야하며
  데이터 저장공간 자체를 의미하기도함(디스크)
```
## 기본 MySQL SQL 문법
```
Create
INSERT INTO member (name, email, age) VALUES ('John Doe', 'johndoe@email.com', 30);

Read
SELECT * FROM MEMBER;

Update
UPDATE member
SET age = 35
WHERE name = 'John Doe';

Delete
DELETE FROM member
WHERE name = 'John Doe';

```

## 인덱스
```
  인덱스란 효율적인 데이터 검색과 접근을 지원하기 위한 데이터 구조. 인덱스는 데이터베이스 테이블의 특정 열(컬럼)에 대한 검색을 빠르게 수행하도록 도움

    1. 빠른 검색 속도: 인덱스는 데이터베이스 엔진이 데이터를 검색할 때 해당 열의 값의 위치를 빠르게 찾을 수 있도록 처리 이로 인해 검색 연산의 속도가 향상.
    
    2. 유일성: 인덱스를 생성할 때 고유한(unique) 제약조건을 설정할 수 있으며, 이로써 특정 열에 중복된 값을 가질 수 없도록 처리.
    
    3. 데이터 정렬: 인덱스는 데이터를 정렬하고 유지.
    
    4. 범위 검색: 인덱스를 사용하면 특정 범위의 데이터를 효율적으로 검색. 이는 범위 검색 쿼리, BETWEEN 연산자 등에서 유용
    
    5. 복합 인덱스: 여러 열로 구성된 복합 인덱스를 생성할 수 있어, 여러 열을 조합한 검색도 빠르게 처리 가능.
    
    6. 조인 성능 향상: 인덱스는 조인 연산에서도 성능을 향상시키며, 테이블 간의 관계를 효과적으로 처리

    그러나 인덱스를 사용하는 것은 항상 이점만 있는 것은 아니다. 인덱스를 생성하면 데이터 쓰기(삽입, 업데이트, 삭제)의 속도가 떨어지는 단점이 있으며, 데이터베이스 공간을 차지
```

## SQL의 종류
```
  DML
  - 데이터 조작(CRUD)하는데 사용되는 언어
  - 적용 대상은 테이블의 행 -> DML 사용을 위해서는 테이블이 정의되어 있어야 함

  DDL
  - 데이터베이스, 테이블, 뷰, 인덱스 등의 개체를 생성 / 삭제 / 변경하는 역할
  - 주로 CREATE / DROP / ALTER 등의 DDL 사용
  - DDL은 트랜잭션을 발생시키지 않는다 -> 롤백 불가

  DCL
  - 사용자에게 권한을 부여하거나 빼앗을 때 주로 사용
  - GRANT / REVOKE / DENY등 존재
```
#### 예제
```

SELECT
    DATE_FORMAT(MM.REG_DATE, '%Y-%m-%d') AS 'regtime',
    IF(DATE_FORMAT(MM.REG_DATE, '%i:%s') = DATE_FORMAT(M.JOIN_TIME, '%i:%s'), 'new', 'excha') AS 'convert',
    CASE
        WHEN MM.jp LIKE '%java%' THEN '1a'
        WHEN MM.jp LIKE '%spring%' THEN '2a'
        WHEN MM.jp LIKE '%react%' THEN '3a'
        WHEN MM.jp LIKE '%php%' THEN '4a'
        WHEN MM.jp LIKE '%kotlin%' THEN '5a'
        WHEN MM.jp LIKE '%jas%' THEN '6a'
        WHEN MM.jp LIKE '%html%' THEN '7a'
        WHEN MM.jp LIKE '%sql%' THEN '8a'
        ELSE 'else'
        END AS 'lang',
    M.em AS 'em',
    MM.na AS 'na',
    MM.cp AS 'cp',
    MM.bir AS 'bir',
    M.adr AS 'adr' ,
    CASE
        WHEN MM.GEN IN (1, 3) THEN 'MAN'
        ELSE 'WOMAN'
        END AS 'alGEn',
    IF(M.MGD_ID IS NULL, 'up', 'down') AS 'alpha',
    IF(M.MGD_ID IS NOT NULL, MG.NAME, ' ') AS 'a',
    IF(M.MGD_ID IS NOT NULL, MG.CELL, ' ') AS 'b',
    IF(M.MGD_ID IS NOT NULL, MG.BIR, ' ') AS 'c',
   ,IF((SELECT COUNT(*) FROM pat AS P WHERE P.ID = M.ID
                                                           and ((LEFT(pk,8) <=20231012 and RIGHT(pk,8) >=20231012)
    or(LEFT(mk,8) <=20231012 and RIGHT(mk,8) >=20231012)
    or(LEFT(sk,8) <=20230924 and RIGHT(sk,8) >=20231012)
    or(LEFT(kmk,8) <=20231012 and RIGHT(kmk,8) >=20231012)))>=1,'sub','nor') AS 'subYn'
FROM
    me AS M
        INNER JOIN MAS AS MM ON MM.ID = M.MST_ID
        LEFT JOIN GUA MG on M.MGD_ID = MG.ID
WHERE
    MM.REG_DATE BETWEEN '2023-04-11 00:00:00' AND '2023-10-12 23:59:59'
    and M.DROP_TIME IS NULL
ORDER BY
    MM.REG_DATE ASC

```

## 인덱스 

`데이터베이스 튜닝`
```
  데이터베이스 튜닝이란 SQL서버가 기존보다 더욱 좋은 성능을 내도록 하는 전반적인 방법론을 말한다.

  db튜닝은 두 가지 관점으로 볼 수 있다.

  1. 성능 개선
  - 1분만에 조회되던 쿼리를 10초로 줄이게 된다면 사용자 관점에서는 엄청난 변화라고 느껴질 수 있다
  - 그러나 성능을 개선하는 대신 서버에서 일어나는 일이 100배 늘어난다면 전체적인 시스템 성능은 오히려 나빠질 수 있다

  2. 부하 개선
  - 각각의 사용자에 대해 서버가 처리하는 총 작업량을 줄임으로써
    서버 시스템의 전반적인 성능을 향상시켜 더 프로세스를 수행할 수 있다.

```
### 인덱스의 내부 작동
`사전 지식`
```
  1. B-Tree
  B-Tree는 자류구조에서 나오는 범용적 데이터 구조다.

  이 구조는 주로 인덱스를 표현할 때와 그 외에도 많이 사용된다.
  이름에 알 수 있듯 균형이 잡힌 트리이다.

  트리 구조에서 노드라는 개념이 사용되는데, 노드는 자료구조에서 데이터가 존재하는 공간을 말한다.

  인덱싱이 안되어있는 db에서 자료를 찾기위해 최악의 경우 전체를 조회할 수 있는데,
  정렬이 되어있는 인덱싱 테이블에서 루트페이지로부터 찾고자 하는 데이터의 노드를 찾아 조회를 하여
  효과적인 조회 성능을 낸다.

  조회에서는 큰 성능을 내나 INSERT 발생 시 오히려 성능 저하를 낸다.
  이미 정렬되어있는 B-Tree 노드에 데이터가 추가가 될 경우
  루트부터 리프까지 페이지 분할이 생기기 떄문이다.
  
  
```
