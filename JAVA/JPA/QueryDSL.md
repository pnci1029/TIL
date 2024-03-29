## QueryDSL에서 Impl Custom을 쓰는이유?
```
  - 스프링 data JPA를 사용하며 사용자 정의 쿼리를 함께 사용하기 위함
  memberRepository.searchMember();
  memberRepository.findById(id);
    1. 사용자 정의 인터페이스 생성
    2. 사용자 정의 구현체 생성
    3. 스프링 data JPA에 사용자 정의 인터페이스 상속

  - 핵심 비즈니스 로직으로 재사용 가능성이 높은 쿼리나 엔티티를 조회하는 경우는 Custom에 사용
  - 다만 공용성이 없고 특정 api에 특화된 복잡한 쿼리일 경우
      @Repository
      public class MemberQueryRepository{
      JpaQueryFactory 의존성 주입...
    }

  
```
`그렇다면 굳이 인터페이스를 둘 이유가 있을까? 바로 구현체를 둬도 되지 않을까?
  `
```
  1. 인터페이스를 통해 메소드명을 바로 확인이 가능하고, 한번에 어떤 기능을 하는 기능인지 파악가능

  2. 구현체는 인터페이스가 어떤 기능을 할것인지 정의해놓은 것이지 메소드 명을 통해 기능을 파악하기 어렵다.

  3. 은닉의 기능
```

  - ![스크린샷 2023-11-17 오후 3 43 15](https://github.com/pnci1029/TIL/assets/81909140/636537a2-1cbc-4583-ae10-abcaf1528211)


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
    - fetchCount() : count 쿼리로 변경해서 count 수 조회. 
#. 
#. 
# 동적쿼리 처리방법
  - booleanExpression을 활용한 where 절 활용
  ```
  public BooleanExpression articleEq(String articleName){
    return username != null ? QArticle.name.eq(username) : null;
  }
  
  public BooleanExpression commentEq(String commentName){
    return commentName != null ? QComment.name.eq(commentName) : null;
  } + 
  public BooleanExpression articleAndComment(String articleName, String commentName){
    return QArticle.name.eq(articleName).andQComment.name.eq(commentName);
  }
  -> 모듈화가 가능하다.
  ```


