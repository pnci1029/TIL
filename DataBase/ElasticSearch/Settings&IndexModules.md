## Settings Basic
  - 대부분의 경우 엘라스틱 서치 기본 세팅을 가져가는게 좋으나, 세팅 우선순위나 추가 설정이 필요한 경우 사용할 수 있다.
  - <img width="860" alt="스크린샷 2023-06-24 오후 2 01 36" src="https://github.com/pnci1029/TIL/assets/81909140/1f6ef669-fbc6-4e5e-8d24-ad18a681bcea">
#  
#  
## 샤드 할당 테스트
  - 엘라스틱 서치 인스턴스 2개 실행 후 각각 attribute, tier 두개의 설정으로 테스트
  ```
    shard1 (es1 인스턴스)

    vi/config/elasticsearch.yml

      cluster.name: fastcampus-data-tier
      cluster.routing.allocation.awareness.attributes: tier
      node.name: data-hot
      node.roles: [ "master", "data" ]
      node.attr.tier: hot



    shard2 (es2 인스턴스)
    
    vi/config/elasticsearch.yml

      cluster.name: fastcampus-data-tier
      cluster.routing.allocation.awareness.attributes: tier
      node.name: data-cold
      node.roles: [ "master", "data" ]
      node.attr.tier: cold

  ```
  - 인스턴스당 노드 구성 확인
  - <img width="364" alt="스크린샷 2023-06-24 오후 2 34 27" src="https://github.com/pnci1029/TIL/assets/81909140/ced8b15b-6fe4-44a3-92ba-46fd80ea8cb1">
## api 요청 통해 인덱스 생성
  - <img width="909" alt="스크린샷 2023-06-24 오후 2 41 24" src="https://github.com/pnci1029/TIL/assets/81909140/cf0664be-111e-4ef5-ac52-1b6957eb98d7">
  - 인덱스 생성 샤드, 티어 등 기입 후 put 메소드를 통해 요청 (/shard-allocation-00001 니 마음대로)
  #  
  #  
  - <img width="541" alt="스크린샷 2023-06-24 오후 2 42 13" src="https://github.com/pnci1029/TIL/assets/81909140/743d6f9c-1c82-4502-a653-5e3c304f5376">
  - 요청 티어에 매칭되는 생성 인덱스 확인 (/_cat/shards/shard-allocation-00001)
### 생성된 인덱스 수정
  - 생성된 샤드 할당번호를 수정 요청으로 요청
  - <img width="730" alt="스크린샷 2023-06-24 오후 2 46 43" src="https://github.com/pnci1029/TIL/assets/81909140/aeec44fe-2509-48a0-8ec0-4c98e5f6b980">
  - 
  - <img width="515" alt="스크린샷 2023-06-24 오후 2 48 21" src="https://github.com/pnci1029/TIL/assets/81909140/15633fa7-2402-45ee-b4a2-4afb514b88ec">
#  
#  
#  
## 인덱스 모듈
  - 개별 인덱스에 대한 제어와 운영
  - <img width="1000" alt="스크린샷 2023-06-24 오후 3 36 01" src="https://github.com/pnci1029/TIL/assets/81909140/54bf9e1a-7ba9-4047-84f2-d14cbb799c1a">
  ```

    static 설정
      - shard를 통해 인덱스를 할당(allocation)하여 생성하는 인덱스
        (http://localhost:9200/shard-allocation-00001)

    dynamic 설정
      - 인덱스 설정 이후 shard에 Setting 이라는 명령을 통해 reAllocation이 적용된 인덱스
        (http://localhost:9200/shard-allocation-00001/_settings)

  ```





