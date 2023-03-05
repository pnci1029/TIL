## Metrics 설정 및 응답
### 톰캣 메트릭스
```
# 톰캣 메트릭 활성화
server:
  tomcat:
    mbeanregistry:
      enabled: true

http://localhost:8080/actuator/metrics 내 톰캣 메트릭스 추가 활성화
    "tomcat.cache.access",
    "tomcat.cache.hit",
    "tomcat.connections.config.max",
    "tomcat.connections.current",
    "tomcat.connections.keepalive.current",
    "tomcat.global.error",
    "tomcat.global.received",
    "tomcat.global.request",
    "tomcat.global.request.max",
    "tomcat.global.sent",
    "tomcat.servlet.error",
    "tomcat.servlet.request",
    "tomcat.servlet.request.max",
    "tomcat.sessions.active.current",
    "tomcat.sessions.active.max",
    "tomcat.sessions.alive.max",
    "tomcat.sessions.created",
    "tomcat.sessions.expired",
    "tomcat.sessions.rejected",
    "tomcat.threads.busy",
    "tomcat.threads.config.max",
    "tomcat.threads.current"
```
#### tomcat.threads.config.max
  - 동시에 처리 가능한 최대 고객의 요청 수 확인
  - 로컬에서 테스트 상 200개
```
http://localhost:8080/actuator/metrics/tomcat.threads.config.max

"name": "tomcat.threads.config.max",
  "description": null,
  "baseUnit": "threads",
  "measurements": [
    {
      "statistic": "VALUE",
      "value": 200.0
    }
  ],
```
#### tomcat.threads.busy
  - 현재 스레드 중 동작중인 스레드 수
  - 로컬에서 테스트 상 1개
```
{
http://localhost:8080/actuator/metrics/tomcat.threads.busy

  "name": "tomcat.threads.busy",
  "description": null,
  "baseUnit": "threads",
  "measurements": [
    {
      "statistic": "VALUE",
      "value": 1.0
    }
  ],
```
#### tomcat.threads.busy 수 > tomcat.threads.config.max 가 된다면?
  - 장애 발생
  - 모니터링 툴을 통해 확인 후 미리 조치 필요
