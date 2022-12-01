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
      
  
*. 스프링 빈 등록 방법?
  - 
 
 
*. 빈 생명주기?
  - 
 
 
*. IOC와 DI
   - 
   - 11
 
*. Configuration vs Component vs Bean?
  -
  - Bean
    - 주로 메소드 상단에 @Bean 부여
      DI 컨테이너에 해당 메소드의 **반환객체**가 등록됨
      
      
      
      
      
