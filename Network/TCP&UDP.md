# 왜 알아야 할까?
  - DB 서버와 통신하는 과정에 데이터가 소실이 되거나 순서 변형 발생 시 큰 문제 발생
  - 웹어플리케이션의 신뢰성과 성능에 중요한 역할
## TCP / IP 모델
```
Application Layer             - 웹 브라우저(http)
Transport Layer               - TCP / UDP
Internet Layer                - IP
Network Acess Layer           - 인터넷
```
## TCP 동작원리
  1. 소켓 생성
  2. 3 Way HandShake (연결)
  3. 데이터 송 수신
  4. 4 Way HandShake (연결 종료)
