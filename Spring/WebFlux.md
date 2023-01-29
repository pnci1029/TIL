# Spring WebFlux?
  - ![다운로드](https://user-images.githubusercontent.com/81909140/215332760-776dcecb-b551-43ec-b6c6-bd346e15a28e.png)
  - client, server에서 리액티브 스타일의 어플리케이션 개발을 도와주는 스프링 모듈
  - 비동기 논블로킹 처리 방식
  - 비동기 처리를 하기 때문에 Spring mvc와 비교하여 대량의 요청을 빠르게 처리 가능
  - 요청을 Event-Driven 방식으로 처리
  - 이벤트 루프가 돌아서 요청이 발생할 경우 그것에 맞는 핸들러에게 처리를 위임하고 처리가 완료되면 callback 메소드 등을 통해 응답을 반환
```
  Spring MVC                    Spring WebFlux
  - Sync - Blocking 방식         - Async - Non Blocking 방식
  - Thread Pool 요청처리 방식      - Event-Driven 요청처리 
```
