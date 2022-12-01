*. 스프링 빈이란?
  - 스프링 컨테이너에서 관리하는 객체

*. 스프링 빈이 필요한 이유?
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
 

 *. IOC와 DI
   - 
 
*. 컴포넌트와 빈의 관계?
  - 
