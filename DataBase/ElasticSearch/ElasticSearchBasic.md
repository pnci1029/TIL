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
## 엘라스틱 서치 basic
  - 기본 컴포넌트 구성
  - <img width="675" alt="스크린샷 2023-06-24 오후 1 36 26" src="https://github.com/pnci1029/TIL/assets/81909140/60645d1f-35ee-4b65-ab2a-cdfebd66d79e">
  - 
    - Cluster
    ```
  
      Cluster
      - cluster.name이 가장 중요
      - 기본 값은 elasticSearch
      - cluster 구성 시 node역할에 따른 구성 필수
      - master node에 대한 quorum 구성 필수
  
        클러스터 구성 시 중요 설정
        cluster.name:
        discovery.type: 싱글 노드 구성 시 설정 (cluster.initial_master_node 설정과 동시에 구성 불가)
        discovery.seed_host: 
        cluster.initial_master_node:
    ```
    - Node
    - <img width="944" alt="스크린샷 2023-06-24 오후 1 47 37" src="https://github.com/pnci1029/TIL/assets/81909140/67dc705e-9f75-4d6e-be58-a786eb956422">
    ```
  
      Node
      - 엘레스틱 서치 인스턴스가 시작할때마다 실행
      - 노드들의 모음이 Cluster
      - 단일 노드로도 실행 가능(=단일 노드 클러스터)
      - 기본설정
        node.name:
        node.rolse:
  
    ```
    - Index
    ```
    
      index
      - 분산된 Shard에 저장된 문서들의 논리적 집합
      - Lucene 기준의 index를 엘라스틱 서치에서는 shard라고 함
      - Primary shard와 Replica shard로 구성되며 Data Node에만 위치
    
    ```
     - Shard
    ```
    
      shard
      - 물리적인 데이터가 저장되어 있는 단위
      - 인덱싱 요청이 있을 때 분산된 위치에 있는 노드를 샤드로 문서를 색인
      - 인덱스의 샤드는 각 노드에 따른 역할 분배 가능
    
    ```
    #
    #  
  - 엘라스틱 서치는 jvm 영역에서 실행되기 때문에 heap 설정이 필요하다
  - 시스템 메모리를 안정화하여 사용하기 위해 다음과같은 설정 필요
    ```
    
      bootstrap.memory-lock: true       => 엘라스틱 서치는 http, transport 통신 둘다 지원. 노드간 통신은 transport로 이루어지며 통신을 위한 port와 content 전송에 따른 설정 가능
    
      http:port:9200                    => 기본 9200 포트로 지정되며 지정된 포트번호로 할당
    
      http.max_content_length           => rest api 요청 시 실제 데이터가 크거나 파일이 100MB가 넘는 경우 조절 처리
    
      http.cors.enabled                 => 기본값은 false, true로 지정할 경우 허용할 orgin 등록 필요

    ```
#  
#  
refered by (https://www.elastic.co/kr/downloads/)



