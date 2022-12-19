*. 프레임워크 vs 라이브러리
  -
  - 프레임워크가 제어권을 갖고 내가 작성한 코드를 프레임워크가 적절한 시기에 호출한다면 프레임워크
    - 프레임워크의 생명주기를 따른다 -> 빈 생명주기
  - 개발자가 제어권을 갖고 호출을 할 수 있다면 라이브러리

  
#  
#
*. DI?
  -
  - 실행 시점에 클라이언트 객체(MemberService) 외부에서 구현 객체(AppConfig)가 생성되어 클라이언트와 서버간 의존관계가 연결되는 것
  - 어플리케이션 실행 시점 이전에는 구현객체를 클라이언트 시점에서 알 수 없음
  
#  
#

*. IOC / DI 컨테이너?
  -
  - 클라이언트 외부에서 의존관계를 연결해주고 객체를 관리해주는것  
#  
#
*. 스프링컨테이너?
  - 
  -  파라미터로 넘어온 설정클래스(appconfig)를 사용해 스프링 빈 등록, 보관
  -   * 싱글턴 컨테이너 (JVM 안에 각 객체는 하나씩만 존재 가)
  - 스프링 컨테이너 생성과정
    1. 스프링 컨테이너 생성(AppConfig.Class)
    2. 스프링 컨테이너 내 (key(빈 이름) : value(반환 인스턴스 객체)) 형식으로 빈 등록
    ```
    ex)
    @Bean
    public MemberSertvice memberService(){
      return new MemberServiceImpl(memberRepository);         -> key(memberSertivce) : value(MemberServiceImpl);
    }
    @Bean
    public MemberRepository memberRepository(){
      return new JPARepository();                             -> key(memberRepository) : value(JPAReppsitory);
    }
    ```
    3. 스프링 컨테이너 내 빈 의존관계 등
    
    
    
    
    
    
