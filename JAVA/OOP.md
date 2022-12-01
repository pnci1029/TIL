
* 객체지향이란?
  - 객체들의 모임 && 객체들간의 메세지를 통한 프로그래밍
  - 유연하고 변경이 용이

* SOLID란?
  - 좋은객체지향 설계를 위한 5원칙
    - OCP : 개방-폐쇄 원칙 -> 확장에는 열려있으나, 변경에는 닫혀있어야한다
      - 로미오 역할을 구현하는 배우는 바뀌어도 상관이 없다.(확장)
      - 인터페이스를 구현한 클래스를 다수 만들어도 기능에 변화가 안생김
      ```
      public class MemberService{
      
      // private MemberRepository memberRepository = new MemoryMemberRepsotiroy;
      private MemberRepository memberRepository = new CrudRepository;
      }
      ```
      클라이언트(memberservice)에서 기능 클래스를 직접 선택 -> OCP 원칙 위배
      
      ```
      public class MemberService{
      
      @Autowired
      private MemberRepository memberRepository;
      }
      ```
      DI(의존 관계 주입) 컨테이너를 통해 문제 해결

    - DIP : 의존관계 역전 원칙
    - LSP : 리스코프 치환 원칙
    - ISP : 인터페이스 분리 원칙
    - SRP : 단일 책임 원칙


* 객체지향의 특징과 비교
  - 다형성 (역할 <-> 구현 관심사 분)
           (자동차<-> k3) 구현체가 바뀌어도 영향X
           
           G
            -> 클라이언트는 역할에만 관심O
            -> (전기차 <-> 휘발유) 클라이언트는 내부구조에 영향을 주지 않음 && 내부구조가 바뀌어도 영향X
            
            B
            -> 역할(인터페이스)가 바뀌면 클라이언트 + 서버에 큰 영향을 미침(자동차역할 <-> 비행기역할)
            
  
*
  - 

기
```
public interface memberRepository extends JPARepository<Member,Long>

```
