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

  
  
  
  reffered by https://wraithkim.wordpress.com/2017/04/13/java-8-%EC%8A%A4%ED%8A%B8%EB%A6%BC-%ED%8A%9C%ED%86%A0%EB%A6%AC%EC%96%BC/
