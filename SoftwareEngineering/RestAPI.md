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
  **Uniform Interface**
    -> 1. Identification of resources : 리소스가 Uri로 식별가능한지
    -> 2. Manipulation of resources through representations : 서버가 클라이언트가 이해가능한 형태로 응답을 하는지 
    주로 잘 못지키는 규약
     -> 3. Self Descriptive messages : 응답만 보고 응답의 모든 요소를 확인할 수 있는지
     
  ```
  - 
  
