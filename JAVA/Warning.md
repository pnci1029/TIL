*. 컨트롤러에서 응답 시 엔티티 반환 X
  - 
  - 양방향 연관관계 관련 무한루프에 빠질 수 있음(toString 사용 자)
  - 
#  
`NULL, BLANK, EMPTY 차이`
```
  밸리데이션 관련 테스트 코드 작성시

  @NotBlank
  @NotEmpty
  @NotNull
  위 3가지 어노테이션을 자주 사용한다.

  헷갈리는 부분이고 어떤 상황에서 각각 통과가 가능할까?

  String a = null / "" / "     " (공백) / "aaa";
  1. @NotNull 인 경우
  a가 "", "     ", "aaa" 세 경우 통과
   -> a = null 인 경우를 거름

  2. @NotEmpty 인 경우
  a가 "     ", "aaa" 두 경우 통과
   -> a = "" 인 경우를 거름

  3. @NotBlack 인 경우
  a가 "aaa"인 경우만 통과
   -> a = "      " 인 경우를 거름


  * @NotBlack 어노테이션이 문자열인 경우에 주로 사용될 가능성이 높다.
```
