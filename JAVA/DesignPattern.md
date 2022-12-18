*. 싱글톤 패턴
  - 
  - 클래스의 인스턴스가 단 1개만 생성되도록 보장하는 디자인패턴
  - 
  - 같은 요청 반복시 문제 발생 -> 요청할때마다 새로운 객체가 생성
    -  Request(articleService) -> Response(new ArticleService1)
    -  Request(articleService) -> Response(new ArticleService2)
    -  Request(articleService) -> Response(new ArticleService3)
    ![화면 캡처 2022-12-02 154534](https://user-images.githubusercontent.com/81909140/205232159-125f542c-c709-4c09-a19b-5bb042e983da.png) 
    - ㅁ  
    #  
    #
    - 싱글톤 패턴 주의점
      - 싱글톤 방식은 여러 클라이언트가 하나의 인스턴스 객체를 공유하기 때문에 상태를 유지해서는 안됨 -> stateless로 설계
      - 클라이언트가 필드를 변경할수 있으면X
      - 필드에 공유값이 있으면 안
      - ![singleton](https://user-images.githubusercontent.com/81909140/208279364-9f2e4fbc-0bb3-4502-8e9d-2143dc5e963b.png)
        - 싱글톤 내부에 price 필드가 공유됨  
      - ![singletone2](https://user-images.githubusercontent.com/81909140/208279368-5e0fe297-a8b8-441c-b7d5-1023a4da04d6.png)
        - 결과적으로 userA와 userB의 price 필드가 공유됨으로써 userA와 userB의 price 필드값이 같
