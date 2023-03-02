# 스트림 동작원리
  ```
  List<String> myList =
    Arrays.asList("a1", "a2", "b1", "c2", "c1");
 
  myList
      .stream()
      .filter(s -> s.startsWith("c"))
      .map(String::toUpperCase)
      .sorted()
      .forEach(System.out::println);

  // return C1 & C2
  
  
  Stream.of(“a1”,”a2",”a3")
    .map(s -> s.substring(1)) // ["1", "2", "3"]
    .mapToInt(Integer::parseInt) // [1, 2, 3]
    .max() // 3
    .ifPresent(System.out::println); // 3 출력
  ```
  - 리스트 값들을 루프를 돌면서 꺼내어 조건을 만족하는경우 다음 단계로 이동
  - filter /  map 등과 같이 스트림 연산들로 연결된 형태 (연산 파이프라인 이라고 함)
  - 대부분의 스트림 연산들은 람다 표현식을 매개변수로 받음  
#  
#
  ```
  Arrays.asList("a1", "a2", "a3")
      .stream()
      .findFirst()
      .ifPresent(System.out::println);  // a1
  ``` 
  - 스트림 객체를 생성하지 않고 컬렉션과 같은 원본데이터에서 직접 생성 가능
  - 메소드의 이름과 반환값이 생략된다(익명 함수 (annonymous function))

# 람다식
  - 함수형 프로그래밍 패러다임을 지원하기 위해 자바 8부터 추가된 기능
  - 함수를 간단한 식으로 표현하는 방법
  - 람다식은 익명 함수의 형태로, 코드를 간결하게 작성할 수 있게 해줍니다.
  - (parameter) -> { body } 형태로 작성
  ```
  int max(int a, int b){
    if(a>b)return a;
    else return b;
  }
  
  int max(int a, int b) {
  	return a > b ? a : b ;
  }
  ``` 
 
 
  #  
  #  
  #  
  reffered by https://wraithkim.wordpress.com/2017/04/13/java-8-%EC%8A%A4%ED%8A%B8%EB%A6%BC-%ED%8A%9C%ED%86%A0%EB%A6%AC%EC%96%BC/
