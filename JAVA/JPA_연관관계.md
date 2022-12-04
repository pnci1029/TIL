
*. 양방향 연관관계?
  - 
  - ㅁㅁㅁ
  
  - Member 객체와 Order 객체가 있다고 했을 때...
  ```
  1. Order order = em.find(Order.class, 1L);
  2. Long targetId = order.getMemberId(1L);
  3. Member member = em.find(Member.class, targetId);
    -> Order 객체에서 memberId를 찾고 그 memberid로 Member객체에 유저를 찾음(**관계형 db에 맞춘 설계**)

  1.  Order order = em.find(Order.class, 1L);
  2.  Member member = order.getMember(1L);
    -> Order 객체에서 Member 객체 호출(**객체지향적 설계**)
  ```
  - 연관관계 매핑
  ```
  양방향 매핑 이후
  <Member 객체>
  private Long id;
  private String name;
  ~~private Long teamid~~;
  @ManyToOne
  @JoinColumn(name = "team_id")  //컬럼 네임에 pk값 입력
  private Team team;
  }
  
  <Team 객체>
  private Long id;
  private String name;
  **@OneToMany(mappedBy = "team")    => "team"은 Member 엔티티에 변수명 의미 Team <<team>> 이놈
  private List<Member> members = new ArraysList<>();**
  ```
  ```
  매핑 이전
  public class Member{
  
  private Long id;
  private String name;
  private Long teamid;
  }
  
  public class Team{
  
  private Long id;
  private String name;
  }
  ```
  ```
  단방향 매핑 이후
  <Member 객체>
  private Long id;
  private String name;
  ~~private Long teamid~~;
  @ManyToOne
  @JoinColumn(name = "team_id")  //컬럼 네임에 pk값 입력
  private Team team;
  }
  
  ```
  - 
  - 
  - 
  - 
  - **연관관계의 주인**
    - 주인인쪽은 mappedBy 속성 정의 X
    - 주인이 아닌쪽은 mappedBy로 주인 지정(ex) mappedBy = "team")
    - **외래키가 있는곳을 주인으로 지정 (1:N에서 N 쪽이 연관관계의 주인) **
    ```
    - 연관관계의 주인은 Member.team
    member.team -> 조회 / 수정 가능
    team.members -> 조회는 가능 / 수정 X
    ```
    - 
    - 
    - 
    - ㅁ
    - 자주 하는 실수
    ```
    <Member>객채와 <Team>객체 중 <Member>객체가 연관관계의 주인일 때
    Team team = new team();
    Member member = new Member();
    
    member.setName("member1");
    team.setTeam("team1");
    
    XXXXX   team.getMember.add(member) -> Team 객체가 연관관계의 주인이 아니기 때문에 DB에 저장되지않음(null값으로 등)
    OOOOO   member.setTeam(team)   -> 올바른 사용 (연관관계의 주인 객체에서 서브 객체로 접)
    
    ```
  
  - 단방향 매핑만으로 연관관계 설정이 사실상 완료 (1:N일 때 N(연관관계 주인)에 참조할 객체 컬럼 생성 완료)
    - 단방향 <-> 양방향 둘 다 DB에 영향X
  
