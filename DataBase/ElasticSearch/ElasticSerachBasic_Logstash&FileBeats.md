# Logstash
  - 다양한 소스데이터를 가공하여 엘라스틱 서치에 적재하는 도구
  - fileBeats에 비해 무거움
  - 다양한 input, filter, output의 파이프라인 구조를 가짐
    ```
    
      1. input 데이터 메세지 수집
      2. filter에서 input으로 부터 받은 데이터 가공
      3. 가공한 데이터를 output으로 응답
    
    ```
  - 자원을 무겁게 사용하기 때문에 Agent로 사용보단 데이터를 가공/적재하는 Ingestor 역할로 사용 권장
  - <img width="1217" alt="스크린샷 2023-06-23 오후 10 14 16" src="https://github.com/pnci1029/TIL/assets/81909140/3a2f669d-7bd2-47f6-a6bb-95203d214b1f">
#  
#  
#  
#  
# FileBeats
  - <img width="693" alt="스크린샷 2023-06-23 오후 10 15 17" src="https://github.com/pnci1029/TIL/assets/81909140/41ab2fb3-2153-4782-ae7e-42978d8a4802">
  - <img width="589" alt="스크린샷 2023-06-23 오후 10 15 12" src="https://github.com/pnci1029/TIL/assets/81909140/302e1ea7-e1d7-40ad-9664-ee0302a8d331">
  - vi filebeat-eslog.yml
  ```

            enabled: true
            paths:
              - /Users/여기에/파일비츠경로가아니라/엘라스틱서치/경로+/logs형태로 작성해야함/elasticSearch/training/ch1/elasticsearch-7.15.0/logs/*.json
          
          json.keys_under_root: true
          json.add_error_key: true
          json.message_key: log
          
          filebeat.config.modules:
            path: ${path.config}/modules.d/*.yml
            reload.enabled: false
          
          setup.ilm.enabled: false
          setup.template.enabled: false
          
          output.elasticsearch:
            hosts: ["localhost:9200"]
            protocol: "http"
            index: "filebeat-es-%{+yyyy.MM.dd}"
          
          #output.logstash:
            #hosts: ["localhost:5044"]
          
          processors:
            - decode_json_fields:
                fields: ["message"]
  ```
  - yml 작성 후 해당 yml 기반으로 파일비츠 실팽
  ```
    1. 엘라스틱서치 실행 bin/elasticsearch
    2. 키바나실행 bin/kibana
    3. 로그스태시 / 파일비츠 실행 ./filebeat -e -c filebeat-eslog.yml
  ```
  - 키바나 대시보드에서 인덱스 생성
  - <img width="1168" alt="스크린샷 2023-06-23 오후 10 28 56" src="https://github.com/pnci1029/TIL/assets/81909140/0ce60e5f-b697-4ed4-908d-6d3758b4bef8">

