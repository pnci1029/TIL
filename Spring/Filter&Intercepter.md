# 필터
  - (디스패처)서블릿이 제공하는 기능
  ```
  ex) 로그인된 사용자만 볼 수 있는 페이지를 url을 직접 호출했을 때 로그인하지않은 사용자도 접근 가능
  
  AOP로 처리도 가능하지만 웹과관련된 공통 관심사는 서플릿필터나 스프링인터셉터를 사용하는게 좋다
  ```
### 필터의 흐름
  ```
    HTTP 요청 -> WAS -> 필터 -> 서블릿 -> 컨트롤러
  
  필터 제한
    HTTP 요청 -> WAS -> 필터 -> 서블릿 -> 컨트롤러 (로그인한 사용자)
    HTTP 요청 -> WAS -> 필터 (적절하지 않은 요청이라 판단, 서블릿 호출X) (비로그인 사용자)
    
  필터 체인
    HTTP 요청 -> WAS -> 필터1 -> 필터2 -> 필터3 -> 서블릿 -> 컨트롤러 (로그 남기는 필터1, 로그인 여부 판단 필터2 ....)
    
  일반적으로 dofilter 통과 후 -> 필터2 -> 필터3 -> 필터가 없을 경우 -> 서블릿 -> ....

  ```
#  
#  
# 인터셉터
  - 디스패처 서블릿과 컨틀롤러 사이에서 동작
  - 서블릿에 대비하여 매우 정밀하게 설정 가능
### 필터의 흐름
  ```
    HTTP 요청 -> WAS -> 필터 -> 서블릿 -> 스프링 인터셉터 -> 컨트롤러
    
    인터셉터 제한
    HTTP 요청 -> WAS -> 필터 -> 서블릿 -> 스프링 인터셉터 -> 컨트롤러 (로그인한 사용자)
    HTTP 요청 -> WAS -> 필터 -> 서블릿 (적절하지 않은 요청이라 판단, 컨트롤러 호출X) (비로그인 사용자)
    
    인터셉터 체인
    HTTP 요청 -> WAS -> 필터1 -> 필터2 -> 필터3 -> 서블릿 -> 컨트롤러 (로그 남기는 인터셉터1, 로그인 여부 판단 인터셉터2 ....)
  ```
  - <img width="700" alt="스크린샷 2023-04-01 오후 1 27 40" src="https://user-images.githubusercontent.com/81909140/229265564-c63316be-e4dc-4f9a-b8cd-0b34fb2e3560.png">
  ```
  일반적인 흐름
    was -> filter(Dispatcher Servlet) -> preHandle ->
    Handler Adapter -> Model&View return ->
    postHandle(Model&View 포함) -> Model 호출 -> after Completion
    
  스프링 인터셉터 예외 발생
    was -> filter(Dispatcher Servlet) -> preHandle ->
    Handler Adapter -> Model&View return ->
    예외 전달 -> was
  ```

  
    
