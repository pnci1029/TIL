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
## 프로메테우스 설정
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
  
  
