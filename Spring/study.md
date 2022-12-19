*. 프레임워크 vs 라이브러리
  -
  - 프레임워크가 제어권을 갖고 내가 작성한 코드를 프레임워크가 적절한 시기에 호출한다면 프레임워크
    - 프레임워크의 생명주기를 따른다 -> 빈 생명주기
  - 개발자가 제어권을 갖고 호출을 할 수 있다면 라이브러리


*. DI?
  -
  - 실행 시점에 클라이언트 객체(MemberService) 외부에서 구현 객체(AppConfig)가 생성되어 클라이언트와 서버간 의존관계가 연결되는 것
  - 어플리케이션 실행 시점 이전에는 구현객체를 클라이언트 시점에서 알 수 없음


*. IOC / DI 컨테이너?
  -
  - 클라이언트 외부에서 의존관계를 연결해주고 객체를 관리해주는것


*. 스프링 빈이란?
  -
  - 스프링 컨테이너에서 관리하는 객체


*. 스프링 빈이 필요한 이유?
  -
  - 관심사 분리(구현체 vs 역할)
      ```
      public class Musical{
      
      @Autowired
      public Musical(Actor actor, Actress actress)
      this.actor = actor;
      this.actress = actress;
      }
      ```
      클라이언트(musical 클래스)에 인터페이스(Actor & Actress)만 의존 ->SOLID의 OCP & DIP 원칙 준수
      actor와 actress가 어떤 구현클래스를 상속받을지 클라이언트는 알 수 없다.
      
      뮤지컬은 무대는 역할에만 의존하고 어떤 배우가 올지는 알수없
      
   - **스프링 빈 상속관계**
     
      
  
*. 스프링 빈 등록 방법?
  - 
 
 
*. 빈 생명주기?
  - 
  - 스프링 컨테이너 생성 - 빈 등록 - 의존관계 주입 - 초기화 콜백 - 빈 사용 - 소멸전 콜백 - 스프링 종료
  - 스프링에서 초기화 / 소멸전 콜백 지원 방법
    1. 인터페이스(InitializingBean, DisposableBean)
      - InitializingBean, DisposableBean 인터페이스 상속받아 사용  
    2. 설정 정보에 지정
      - @Bean(initMethod = "init", destroyMethod = "close") 
    3. @PostConstruct, @PreDestroy 어노테이션 사용 
      - 가장 권장되는 방법
      - 스프링에 종속되는 기술이 아니고 자바 표준 기술 
      - 다만 외부 라이브러리에서 사용 불가 
 
 
*. IOC와 DI
   - 
   - 11
 
*. Configuration vs Component vs Bean?
  -
  - @Bean
    - 주로 메소드 상단에 @Bean 부여
      어플리케이션 실행 시 스프링 컨테이너에 해당 메소드의 **반환객체**가 등록됨
        -> 스프링 컨테이너에 아래 형식으로 관리
        ```
            메소드 명(key)        반환객체(value)
            memberService         return MemoryMemberRepository
        ```  
    - 컴포넌트 스캔 시 생성된 빈(자동 생성)과 수동 생성 생성한 빈의 이름이 같을 경우?
      - 수동생성된 빈이 우선권을 갖음 -> 자동빈을 오버라이딩 함 
    - 
        #  
        #  
        #
  - @Configuration
    - 클래스 단위에 붙는 어노테이션
    - 빈 어노테이션이 붙은 메소드들을 가짐
    - @Configuration 클래스 내부에 있는 빈들을 싱글톤 상태를 유지하도록 함
      1. 스프링이 cglib이라는 바이트코드를 조작하는 라이브러리를 사용
      2. AppConfig 클래스를 상속받는 AppConfigcglib 클래스를 만들어 반환
      3. ![configuration](https://user-images.githubusercontent.com/81909140/208280489-f80da711-384b-4fff-a62a-a97b0dffd701.png)
    - @Configuration 없이 클래스 내부에 @Bean 메소드만 존재한다면?
      - 빈 객체들이 싱글톤 보장이 되지않는다.
      ```
      ex)
      1. 빈이 존재하지않을경우 -> 빈 생성
      2. 빈이 존재할 경우      -> 존재하는 빈 객체 반환
      3. 싱글톤 패턴 유지
      ```
    - 주의사항
      - @Configuration 클래스는 final 이 되면 안된다. 
      - @Bean 메소드는 final / private 이 되면 안된다. 
        
        
      #  
      #
  - @Component
    - 프로젝트 시작 시점에 @Component 어노테이션이 붙은 클래스들을 빈으로 등록 
      - 그렇다면 스프링 컨테이너 내에 있는 빈들간 의존성 주입은 어떻게?
      ```
      1. @Autowired 사용
       -> 컴포넌트 클래스의 생성자에 해당 어노테이션을 추가함으로써 자동 의존성 주입 
      ```
    - @ComponentScan 시 @Configuration, @Controller, @Service, @Repository 등과 같은 어노테이션이 붙은 클래스들을 자동으로 스프링 컨테이너에 빈으로 등록 
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
    
    
    
    
    
    
