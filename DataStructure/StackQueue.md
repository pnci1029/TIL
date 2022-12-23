# Stack vs Queue
- 비교
  ```
  Stack                                       Queue
  후입 선출                                   선입 선출
  ex)브라우저 뒤로가기 & 실행취소              ex) 프로세스가 있는 작업(은행작업) & 우선순위 작업 
  
  클래스로 정의되어 있음                      인터페이스로 정의되어 있음 -> 구현체 찾아 객체생성
  ->Stack<Integer> stack = new Stack<>();    -> Queue<Integer> queue = new LinkedList<>();
  ```
  - 메소드 비교
  ```
  Stack                                      Queue
  .push - 스택에 값 저장                      .offer - 큐에 값 저장 -> true / false 로 결과값 반환
   (.add)도 사용 가능하나, 큐나 배열과         vs(.add)             -> 실패할경우 예외 발생
   구분을 위해 push 사용 권장
   
  .pop - 제일 마지막에 들어온 객체 반환       .poll - 가장 먼저 들어온 객체 반환
  (비어 있을 시 예외 발생)
   
  .peek - 가장 먼저 반환될 값 출력            .peek - 가장 먼저 반환될 값 출력
  (후임 선출 기준)                            (선입 선출 기준)
  ```
  - ![stackqueue](https://user-images.githubusercontent.com/81909140/209307415-e231f66e-d1fa-4a87-b937-82ab2481935b.png)   결과값 : ![stackqueue2](https://user-images.githubusercontent.com/81909140/209307438-39116388-76e0-4909-a63d-37493a55ab87.png)

