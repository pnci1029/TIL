# RestApi?
  - Rest 아키텍처 스타일을 따르는 Api(REpresentational State Transer)
  - 서로다른 시스템의 독립적인 진화를 보장하는 방법 
  
# 대부분 못지키고 있는 RestApi 규약
  - (참고 https://www.youtube.com/watch?v=RP_f5dMoHFc)
  ```
  Client-Server
  Stateless
  Cache
  Layered System
  Code-on-Demand (optional)
 +
  ```
  -  **Uniform Interface**  
#
    1. Identification of resources : 리소스가 Uri로 식별가능한지
    2. Manipulation of resources through representations : 서버가 클라이언트가 이해가능한 형태로 응답을 하는지
    주로 잘 못지키는 규약
    3. Self Descriptive messages : 응답만 보고 응답의 모든 요소를 확인할 수 있는지
      - ex
      ```
      응답예시 1) X
      {"lang" : "ko"}                     ->  응답 성공 실패 여부에 관련없이 상태를 확인 불가능.
      
      응답예시 2) X
      http/1.1 200 ok
      {"lang" : "ko"}                     -> 상태 확인이 가능하나, 응답 포멧 여부 확인 불가능.
      
      응답예시 3)X
      http/1.1 200 ok
      content-type : application/json     -> 응답 포맷까지 확인가능하나, lang이라는 키값이 의미하는 바를 알수 없음.
      {"lang" : "ko"}
      
      
      응답예시 3) O
      http/1.1 200 ok
      content-type : application/json
      
      {"lang" : "ko",
       "description" : https://www.help.shop} -> 응답받는곳에서 응답 값들을 확인가능한 도메인 첨부(응답값이 모든 요소 확인 가능) 
      ```
    4. HATEOAS(hypermedia as the engine of application state) : 링크를 통해 어플리케이션의 상태전이가 가능해야함 
    - 응답 시 Xml이나 Json + HAL(Hypertext Application Language) 함께 첨부하여 현재 어플리케이션의 도메인, 다음이나 이전 도메인을 통해 상태 전이가 가능  
      
  
