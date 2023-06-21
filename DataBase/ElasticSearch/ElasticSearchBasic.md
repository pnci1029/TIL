# Elastic Serach
  - DBMS와 비교한 엘라스틱 서치
  - <img width="876" alt="스크린샷 2023-06-03 오후 1 18 51" src="https://github.com/pnci1029/TIL/assets/81909140/49605036-afaa-41c8-b001-1c9fd6368b8a">
  - <img width="867" alt="스크린샷 2023-06-03 오후 1 20 31" src="https://github.com/pnci1029/TIL/assets/81909140/410b328b-01dd-446b-9894-a0cf68142fd3">
  ```
  - Lucene 이라는 검색 라이브러리로 만들어진 오픈소스 검색 엔진
  
  - Elastic Stack
    (Elastic Search를 중심으로 한 스택 + Logstash, Kibana, Beats)
    
  - Time Series로 제공되는 데이터도 처리가능
  
  - Key : Value 형태의 NoSQL 엔진으로 활용
  
  - 실시간 조회 및 분석을 요구하는 Speed Layer 현장에서 활용
  
  - RESTful API + Client Library 제공
  
  - QueryDSL을 통한 자체질의문 가능
  
  - JVM 기반으로 실행
  ```
#  
## 엘라스틱서치 설치 및 실행 
#  
  ```
    도커로 실행을 위한 명령어
    1. 디렉토리 생성 후 엘라스틱 사용중인 버전의 엘라스틱 도커 이미지 파일 풀
       docker pull docker.elastic.co/elasticsearch/elasticsearch:8.3.2
       
    2. 이미지 아이디로 실행
       docker run -d -p 9200:9200 -p 9300:9300 -e "discovery.type=single.node" f9e2357efe32

    + 다른버전 명시를 통해서 이미지 다운 후 실행도 가능
      docker run -d -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.12.0
      Unable to find image 'docker.elastic.co/elasticsearch/elasticsearch:7.12.0' locally
      7.12.0: Pulling from elasticsearch/elasticsearch
      0122c235edee: Downloading  32.26MB/84.09MB
      e1f8ca3312e1: Download complete 
      ffd003bc4f38: Download complete 
      f35bf9416ca9: Downloading  69.33

  ```
  - 풀 받은 도커 이미지 확인
  - <img width="1417" alt="스크린샷 2023-06-03 오후 1 46 58" src="https://github.com/pnci1029/TIL/assets/81909140/6e9e4948-7f87-4b90-8078-e363ff323425">
#  
#  
## 엘라스틱서치 구성설정
  - <img width="628" alt="스크린샷 2023-06-03 오후 2 09 08" src="https://github.com/pnci1029/TIL/assets/81909140/b073ee5a-bf4b-4a6b-9c3e-07905473019e">
  - config.yml 설정 수정
  ```
  vi config/elasticsearch.yml
    cluster.name: fastcampus
    node.name: single-node
    discovery.type: single-node
    추가
  ```
#  
#  
### 다중 노드 구성 설정
  ```
    cp -rf elasticsearch-7.15.0 es1
    cp -rf elasticsearch-7.15.0 es2
    cp -rf elasticsearch-7.15.0 es3

    디렉토리에 같은버전 엘라스틱서치 3개 설치


    es1/bin/elasticsearch -d -p PID
    es2/bin/elasticsearch -d -p PID
    es3/bin/elasticsearch -d -p PID
    각 디렉토리의 엘라스틱서치 실행
  ```
  - <img width="922" alt="스크린샷 2023-06-21 오후 9 37 57" src="https://github.com/pnci1029/TIL/assets/81909140/2e007cfb-a1d8-411c-9399-e8bfe9ea94d8">
  ```
    3개의 노드에 별다른 설정없이 실행을 통해 클러스터 구성
  ```
#### 아무 설정이 없는데 어떻게 클러스터 구성이 되었을까?
  - 엘라스틱 서치는 기본적으로 같은 클러스터 네임을 가진 같은 네트워크상의 노드들을 클러스터링 처리를 지원한다.
# Dokcer Compose 를 이용힌 클러스터 노드 설정
  ```
    
  ```

#  
#  
refered by (https://www.elastic.co/kr/downloads/)



