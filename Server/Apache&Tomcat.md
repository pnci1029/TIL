## 아파치
  ```
    - 정적웹 처리에 특화된 웹서버 (HTML, IMG, CSS, JS)
    - 가볍고 안정적이며 사용자의 요구에 따라 설정이 달라질 수 있다.
    - SSL 등 보안프로토콜 지원됨
    - 다양한 운영체제에서 호환됨
    - 웹서버(..+Nginx)
  ```
#  
## 톰캣
  ```
    - 자바 서블릿이나 JSP 등 동적 웹 어플리케이션 처리가 가능
    - 아파치와 함께 사용하여 각각 정적 웹, 동적 웹 처리를 함께 할 수 있다.
    - 데이터베이스와 연동하여 DB에서 데이터를 읽어오는 웹을 개발 할 수 있다.
    - 와스
    
    1. 스프링 웹앱을 war 파일로 빌드 (.class, .jsp 등 파일 압축..)
    2. 톰캣을 사용하여 스프링 서비스 실행
    
    1. 스프링을 톰캣이 들어있는 jar 파일로 빌드
  ```
#  
## 톰캣으로도 웹 서비스 빌드가 가능하지만 아파치나 Nginx랑 함께 쓰는 이유?
  ```
     1. 정적 리소스를 넘겨주는 처리속도가 느리기 때문에?
      -> 톰캣의 정적 리소스 제공 속도가 빨라져서 의미있는 차이가 없음
      
      => 웹서버를 앞단에 두고, 와스를 뒷단에 리버스 프록시로 사용
      => 웹서버로 로드밸런싱
      => 캐싱
      => 와스 작동 여부를 주기적으로 헬스체크
  ```
#  
## 아파치 vs Nginx
  ```
    아파치 -> 다중 프로세스 처리 (컨텍스트 스위칭으로 컴퓨터 자원의 소모 발생)
    Nginx -> 이벤트 처리
  ```