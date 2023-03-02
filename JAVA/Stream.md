# 자바 스트림
  - 자바 8에서 소개된 기능으로, 컬렉션과 배열과 같은 데이터 구조를 처리하는 함수형 프로그래밍 스타일의 API
### 써야하는 이유?
  - 벙렬처리를 통해 대용량 처리 시 효율적이다.
  - 람다식과 결합하여 간결하고 효율적인 코드 작성이 가능하다.
  - 컬렉션의 API를 사용하여 데이터 처리를 하는 경우에는 데이터 처리 로직과 순회 로직이 분리되어 가독성이 좋음
```
        FOR문           vs               Stream
장점     직관적이며 이해가 쉽다.               코드의 가독성이 증가한다.
        기존 자바개발자들에게 익숙함            위에 적혀있는 써야하는이유..
        
단점     대용량 처리 시 속도가 느려질 수 있음     대용량 처리 시 메모리 사용이 늘어날 수 있음
        코드의 길이가 길어지고 가독성이 떨어짐    기존 자바 개발자들에게 익숙치않음
        병렬 처리를 위한 코드가 복잡해질 수 있다.
```
#  
  
### 스트림 생성 -> 중간 연산자 -> 최종연산자
```
import java.util.Arrays;
import java.util.List;

public class Main {
  public static void main(String[] args) {
  
    // 문자열 리스트 생성
    List<String> strings = Arrays.asList("one", "two", "three", "four", "five");

    // 문자열 리스트에서 길이가 3 이상인 문자열 필터링하여 출력
    strings.stream()
      .filter(str -> str.length() >= 3)
      .forEach(System.out::println);

    // 문자열 리스트에서 문자열 길이의 총합 구하기
    int sum = strings.stream()
      .mapToInt(String::length)
      .sum();

    System.out.println("총합: " + sum);
  }
}
```
#  
#  
### 스트림 내장함수 예제
```
filter() : 주어진 조건에 따라 스트림 요소를 필터링합니다.
map() : 스트림 요소를 특정 함수로 변환합니다.
flatMap() : 중첩된 리스트와 같은 구조를 평평하게 펴서 스트림으로 만듭니다.
distinct() : 스트림 요소 중 중복된 것을 제거합니다.
sorted() : 스트림 요소를 정렬합니다.
limit() : 스트림에서 일부 요소만 가져옵니다.
skip() : 스트림에서 일부 요소를 건너뜁니다.
forEach() : 스트림 요소를 반복하여 처리합니다.
reduce() : 스트림 요소를 하나의 값으로 줄입니다.
collect() : 스트림 요소를 컬렉션으로 변환합니다.
allMatch() : 스트림 요소가 모두 주어진 조건을 만족하는지 확인합니다.
anyMatch() : 스트림 요소 중 하나 이상이 주어진 조건을 만족하는지 확인합니다.
noneMatch() : 스트림 요소가 모두 주어진 조건을 만족하지 않는지 확인합니다.
count() : 스트림 요소의 개수를 반환합니다.
findFirst() : 스트림의 첫 번째 요소를 반환합니다.
findAny() : 스트림의 임의의 요소를 반환합니다.

```
#  
#  
### filter() -> 주어진 (filter) 조건을 만족하는 새로운 스트림 반환
```
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David", "Ella");
List<String> filteredNames = names.stream()
                                  .filter(name -> name.startsWith("A"))
                                  .collect(Collectors.toList());
System.out.println(filteredNames); // Output: [Alice]
```
#  
#  
### map() -> 주어진 함수를 사용하여 새로운 스트림 반환
```
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> squaredNumbers = numbers.stream()
                                       .map(number -> number * number)
                                       .collect(Collectors.toList());
System.out.println(squaredNumbers); // Output: [1, 4, 9, 16, 25]
```

#  
#  
### anyMath() -> 일치하는게 하나이상 있는지 확인
```
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
boolean hasEvenNumber = numbers.stream()
                               .anyMatch(number -> number % 2 == 0);
System.out.println(hasEvenNumber); // Output: true
```
#  
#  
### allMatch() -> 주어진 조건이 모두 일치하는지 boolean 값으로 판별
```
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> squaredNumbers = numbers.stream()
                                       .map(number -> number * number)
                                       .collect(Collectors.toList());
System.out.println(squaredNumbers); // Output: [1, 4, 9, 16, 25]
```

#  
#  
### sorted() -> 주어진 배열을 정렬하여 새로운 스트림 반환
```
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
boolean hasEvenNumber = numbers.stream()
                               .anyMatch(number -> number % 2 == 0);
System.out.println(hasEvenNumber); // Output: true
```



