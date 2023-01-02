# QueryDSL vs Native Query vs JPQL
  - aaa

# 사용 시 주의사항
  - 자바 컴파일이나 쿼리dsl 컴파일 빌드 후 생성된 디렉토리 내 Q타입 객체 생성여부 확인
  - 쿼리 요청 시 JPAQueryFactory 클래스로 생성
    - 쿼리문 내 필요 엔티티는 Q타입 클래스로만 요청
  - 
# Fetch Join
  - SQL 에서 제공하는 기능은 아님
  - 연관된 엔티티들을 SQL문 한번으로 조회하는 기능
  - 주로 성능 최적화에 사용
  - Fetch Join 미사용 시
![스크린샷 2023-01-02 오후 7 10 16](https://user-images.githubusercontent.com/81909140/210236485-73cfa779-e87a-4520-83ba-a2f569b8388a.png) | ![스크린샷 2023-01-02 오후 7 10 47](https://user-images.githubusercontent.com/81909140/210236491-a50e1e64-d38d-4454-9cf8-935396c26e86.png)  
#  
#

  - Fetcy Join 사용 시
![스크린샷 2023-01-02 오후 7 11 03](https://user-images.githubusercontent.com/81909140/210236502-afd61c16-4e98-4677-b9fc-150989a656be.png)
![스크린샷 2023-01-02 오후 7 11 37](https://user-images.githubusercontent.com/81909140/210236506-d4647f3e-3d31-4180-afbc-8fa93db3944d.png)

  - Fetch 전략
    - fetch() : 리스트 조회, 데이터 없으면 빈 리스트 반환
    - fetchOne() : 단 건 조회 / 결과가 없으면 : null / 결과가 둘 이상이면 : com.querydsl.core.NonUniqueResultException 발생
    - fetchFirst() : limit(1).fetchOne()
    - fetchResults() : 페이징 정보 포함, total count 쿼리 추가 실행
    - fetchCount() : count 쿼리로 변경해서 count 수 조회
