# Kibana
  - 엘라스틱 서치에 저장된 데이터를 조회하고 분석할 수 있도록 제공하는 도구
  - Elastic Search 공식 Interface
  - 초기 Dashboarfd, Visualization을 위한 도구에서 현재 Elastic Stack 을 운영하고 모니터링 용도로 확대
  ```
    1. 엘라스틱 서치 실행 후 키바나 실행
      키바나 실행 시 실행중인 엘라스틱서치 포트 검색 -> 조회가 안될 경우 에러 발생
  ```
  - ![스크린샷 2023-06-21 오후 10 49 12](https://github.com/pnci1029/TIL/assets/81909140/2bcdad2c-3c00-4995-bda3-15ff723586e0)
#  
  ```
    bin/elasticsearch + bin/kinana

    http://localhost:5601/ 키바나 기본 포트
  ```
  - ![스크린샷 2023-06-21 오후 10 53 22](https://github.com/pnci1029/TIL/assets/81909140/affb16ca-672b-4435-afc0-1937eaccf06d)
  - ![스크린샷 2023-06-21 오후 10 55 19](https://github.com/pnci1029/TIL/assets/81909140/51062bc0-3462-46c0-9b21-f8dc2d11e418)

#  
#  
# 키바나 살펴보기
  ```

    9300포트(엘라스틱서치)에서 요청 데이터를 개발도구로 조회(포스트맨 형태)

  ```
  - <img width="1704" alt="스크린샷 2023-06-23 오후 9 22 13" src="https://github.com/pnci1029/TIL/assets/81909140/35242e2b-dc21-4d97-9d20-6cab525e159e">
  - 
  ```

    도커를 활용하여 키바나 띄우기

  ```
#  
    1. YML파일 정의
    ```
    
      docker-compse-kibana.yml
      
          version: "3.7"
      services:
        docker-kibana:
          image: docker.elastic.co/kibana/kibana:7.15.0
          container_name: docker-kibana
          environment:
            ELASTICSEARCH_HOSTS: '["http://host.docker.internal:9200"]'
          ports:
            - 5601:5601
          expose:
            - 5601
      #    volumes:
      #      - ./kibana-config.yml:/usr/share/kibana/config/kibana.yml
          restart: always
          network_mode: bridge

    ```
    2. 도커 컴포즈 실행 (docker compose -f docker-compose-kibana.yml up)
    - 키바나 버전 이미지 다운로드 후 실행
    - <img width="1535" alt="스크린샷 2023-06-23 오후 9 36 22" src="https://github.com/pnci1029/TIL/assets/81909140/35adc4ce-bac5-41ed-b2a4-07e663597124">

  
