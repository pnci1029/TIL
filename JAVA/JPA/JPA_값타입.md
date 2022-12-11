*. JPA의 데이터타입
  - 
  - 엔티티타입
    - @Entity로 정의하는 객체
    - 식별자를 통해지속적으로 추적가능
         
  - 값타입 (기본 값타입 + 임베디드 타입 + 컬렉션 타)
    - int, String처럼 자바 기본 타입이나  객체
    - 식별자가 없고 값만 있으므로 변경 시 추적 불가 
  - 임베디드타입
    - 
    - 엔티티 내에 공통거나 자주 사용하는 필드값들이 있을 시 클래스로 만들어 사용
    - @Embeddable: 값 타입을 정의하는 곳에 표시
    - @Embedded: 값 타입을 사용하는 곳에 표시
    ```
    <임베디드 값 타입을 사용하는 객체>
    1. 
    @Entity
    public class Member{
    private Long id;
    private String name;
    
    private LocalDateTime startDate;
    private LocalDateTime endDate;
    
    private String city;
    private String street;
    private String zipcode;
    }
    
    2. 
    @Entity 
    public class Member{
    private Long id;
    private String name;
    @Embedded                             @Embedded
    private Period period;                private Address address

    
    @Embeddable                                                     @Embaddable
    public class Period {                                           public class Address {
    private LocalDateTime startDate;                                private String zipcode;   private String city;
    private LocalDateTime endDate;                                  private String street;
}

    }
    ```
