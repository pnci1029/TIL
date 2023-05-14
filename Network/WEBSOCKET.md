# WebSocket
- ![웹소켓1](https://github.com/pnci1029/TIL/assets/81909140/dcccb803-e46d-4ca2-99b5-70af9c270a2d)
  ```
  - 클라이언트와 서버간 양방향 통신을 지원하는 프로토콜
  - 웹소켓 서버 엔드포인트에 연결된 서버와 클라이언트는 계속 상호작용 혹은 데이터 송수신
    - 엔드포인트 ~> 웹애플리케이션에서 서버와 클라이언트간 통신을 위해 정의된 Url
  
  
  
  1. 양방향성 : sse 통신과 달리 서버와 클라이언트간 양방향 통신을 지원
  2. 실시간성 : 서버에서 클라이언트에 실시간으로 데이터 전송 지원
  3. 단일연결 : 최초 한번의 연결로 서버와 클라이언트간 지속적인 연결을 유지
  4. 작은 오버헤드 : 
     - http 통신과 비교하여 웹소켓은 최초 핸드쉐이크 단계에서만 메타데이터를 공유하고, TCP 연결을 유지함으로 http 통신처럼 매번 연결을 새로 시도할필요가 없음
     - 웹소켓의 헤더는 http 헤더보다 훨씬 작다
     - http 통신은 요청 마다 요청이 필요함으로 네트워크 비용이 훨씬 절감된다.
  
  
  
  웹소켓의 HandShake
  (웹소켓 handShake 과정은 전반적인 http 통신과 유사하나, 연결 후 추가적인 데이터 통신을 위한 http 요청이나 응답이 필요없다.)
    1. 클라이언트가 서버에 http 요청. http 헤더에 upgrade 필드를 포함하여 websocket 값 지정
    2. 서버는 클라이언트에 응답 시 upgrade, connection 필드를 포함하여 websocket 값을 지정
    3. 클라이언트는 서버에서 보낸 응답헤더를 확인하여 websocket 프로토콜로 업그레이드가 된 것을 확인하고 통신 연결시작
    
  ```
#  
#  
# Message Broker
  - ![메세지브로커'](https://github.com/pnci1029/TIL/assets/81909140/70d274e5-2512-479f-89bf-10aeacc2aeca)
  - publisher로 부터 받은 데이터를 subscriber에게 전달하는 중간 매개역할
  - 이때 메세지가 저장되는 공간이 Message Queue 이며 메세지 그룹을 Topic 이라 한다.
  - (publisher : 송신자 / subscriber : 수신자 )
  ```
  쉽게 생각하여 메세지를 특정 미들웨어(대표정으로 Apache Kafka, Redis, RabbitMQ, Celery)에 던지고
  이를 필요한 주체가 구독하여 사용 및 처리
  
  
  실시간으로 데이터를 수집하는 rdb가 있을 때 실시간으로 들어오는 정보를 인덱스를 걸어 조회하려면
  insert의 성능이 저하되므로 실시간 처리에 적합하지 않다.
  
  이를 메세지 브로커를 사용하여
  실시간으로 들어온 정보를 Message Queue에 publish 하고, subscribe 하여 바로 사용 하면된다.
  이를 pub/sub 페턴이라고 한다
  
  publisher는 Topic에 메시지를 만들고 publishing 하는 처리를 담당하고, Subscriber는 publishing 된 메시지를 구독하여 읽는 역할을 한다.
  
  
  
  실시간으로 처리할 때 rdb에서 조회하는것과 비교하여 조회 성능이 우수하지만,
  조건처리하여 조회 시 큐에 담긴 메세지를 통째로 조회하기 때문에
  메세지 브로커를 사용하여 조회 시 필터링된 정보만 조회할 수 없다.
  
  따라서 저장 시 필터링하여 적재하거나, Logstash를 이용하여 필터링하여 이용해야한다. 
  ```








#  
#  
#  
(reference https://heodolf.tistory.com/49, https://dev-gorany.tistory.com/3, https://binux.tistory.com/74, https://ellune.tistory.com/29?openLinerExtension=true)
