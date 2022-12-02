*. 싱글톤 패턴
  - 
  - 클래스의 인스턴스가 단 1개만 생성되도록 보장하는 디자인패턴
  - 
  - 같은 요청 반복시 문제 발생 -> 요청할때마다 새로운 객체가 생성
    -  Request(articleService) -> Response(new ArticleService1)
    -  Request(articleService) -> Response(new ArticleService2)
    -  Request(articleService) -> Response(new ArticleService3)
    ![화면 캡처 2022-12-02 154534](https://user-images.githubusercontent.com/81909140/205232159-125f542c-c709-4c09-a19b-5bb042e983da.png) 
    
    
