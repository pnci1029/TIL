## Prometheus
  - 어플리케이션에서 발생한 과거부터 현재까지 메트릭들 이력을 확인할 수 있는 일종의 DB
#  
## Grafana
  - 프로메테우스에 수집된 데이터들을 시각적으로 볼 수 있도록 수 많은 그래프들을 제공
#  
## 전체 프로세스
  - <img width="799" alt="스크린샷 2023-03-06 오후 10 23 31" src="https://user-images.githubusercontent.com/81909140/223122316-9676e249-1649-4bbe-86d4-9a41cdadf8ca.png">
  ```
  1. 스프링부트 액츄에이터와 마이크로미터에서 메트릭들 생성
  2. 프로메테우스에서 생성된 메트릭 수집
  3. 프로메테우스는 수집된 정보를 db에 저장
  4. 그라파나는 프로메테우스에서 수집된 정보들을 조회하여 그래프로 표현
  ```
# 프로메테우스 설정
  1. 어플리케이션 설정 : 어플리케이션 메트릭 정보를 가져올 수 있도록 어플리케이션에서 프로메테우스 설정에 맞춰 메트릭 생성
  2. 프로메테우스 설정 : 프로메테우스가 어플리케이션의 메트릭을 주기적으로 수집하도록 설정
```
프로메테우스는 스프링 액츄에이터 제이슨 형태(/actuator/metrics/...)를 해독 불가 -> 마이크로미터가 해결

(build.gradle)
implementation 'io.micrometer:micrometer-registry-prometheus'
->
/actuator 내 prometheus 추가됨
```
## 프로메테우스 설치파일의 prometheus.yml 에 스크립트 추가
  ```
   - job_name: "spring-actuator"
        metrics_path: '/actuator/prometheus'
        scrape_interval: 1s
        static_configs:
  - targets: ['localhost:8080']
  
  저장 후 터미널에서 다시 실행 -> http://localhost:9090/config 설정 스크립트 추가 확인가능
  ```
#  
### 프로메테우스 이용
  - <img width="1711" alt="스크린샷 2023-03-07 오후 11 15 36" src="https://user-images.githubusercontent.com/81909140/223448222-aba4ecc2-a5c0-4f34-bcc8-e9a1364245bd.png">
  - 단위시간당 요청 수 파악
  - <img width="1710" alt="스크린샷 2023-03-07 오후 11 15 48" src="https://user-images.githubusercontent.com/81909140/223448252-f6a2d71c-20ca-4e8c-abc9-421cc1c8e937.png">
  - 단위시간당 요청 수 그래프로 시각화
  ```
  http_server_requests_seconds_count -> 단위시간당 요청 수 파악
  http_server_requests_seconds_count{uri="/article/log"} -> 특정 uri에 대한 요청 수 파악
  
  자주쓰는 레이블 함수와 쿼리
  
  sum(http_server_requests_seconds_count)
  sum by(method, status)(http_server_requests_seconds_count) SQL의 group by 기능과 유사
  count(http_server_requests_seconds_count)
  topk(3, http_server_requests_seconds_count) 상위 3개 메트릭 조회
  http_server_requests_seconds_count offset 10m  10분전 요청 조회
  
  ```
### 프로메테우스의 게이지와 카운터
##### 게이지
  - 임의로 오르내릴수 있는 값
  - CPU사용량, 메모리사용량, db 커넥션 수
  ```
  system_cpu_usage CPU 사용량 조회
  ```
  - <img width="1708" alt="스크린샷 2023-03-07 오후 11 46 15" src="https://user-images.githubusercontent.com/81909140/223456509-ed179669-7cf9-451d-8d0c-79eebc656d34.png">
#  
#  
#### 카운터
  - 단순하게 증가하는 누적 값
  - HTTP 요청 수, 로그 발생 수
<img width="1721" alt="스크린샷 2023-03-07 오후 11 54 26" src="https://user-images.githubusercontent.com/81909140/223458849-c4d7b01e-fe9f-4a54-8984-411c348d9db8.png">

  ```
  카운터는 계쏙해서 증거하는 그래프 형태라, 특정시간에 요청이 많은지 한눈에 파악하기가 어려움
  -> increase(), range() 함수 사용
  ```
  - increase() 함수 사용 -> (기존 우상향 그래프 ->시간대별로 http 요청 수 파악)
<img width="1708" alt="스크린샷 2023-03-07 오후 11 54 17" src="https://user-images.githubusercontent.com/81909140/223458970-2826d9d3-2972-466e-8574-9d353c9d2227.png">

#  
#  
#  
# 그라파나
  - 순서
    ```
    1. 톰캣 실행
    2. 프로메테우스 실행(터미널 9090)
    3. 그라파나 실행(터미널 3000)
    ```
  - <img width="1444" alt="스크린샷 2023-03-08 오후 11 41 42" src="https://user-images.githubusercontent.com/81909140/223743162-a19bb229-9025-4068-8c72-383920edf8d5.png">
  - 
  - <img width="1653" alt="스크린샷 2023-03-08 오후 11 49 33" src="https://user-images.githubusercontent.com/81909140/223745105-f9b7fc40-b2b7-4587-8341-ed007768c60e.png">
  - 
  ```
  커스텀화 설정 - 패널 명, 단위, 측정값 등등..

  JVM 메트릭
  시스템 메트릭 애플리케이션 시작 메트릭 스프링 MVC
  톰캣 메트릭
  데이터 소스 메트릭
  로그 메트릭
  기타 메트릭

해당값들도 추가가 가능하나 그라파나에서 만들어 둔 대시보드를 사용하면 된다
  ```



  
