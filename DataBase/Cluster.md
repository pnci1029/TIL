# Clustering
  - ![clustering](https://github.com/pnci1029/TIL/assets/81909140/fd7d1fa8-04d2-4887-9d26-79cc44b4661d)

   ```
   DB 스토리지를 공유하고 DB 서버를 다중화 하는 방식
   
   데이터 처리 성능을 향상시키기 위해서 여러 서버를 그룹화 하는 것
   - Active-Active / Active-StandBy 방식 존재
   
   Active-Active
    - 여러대의 서버가 분산하여 트래픽을 받음 (로드밸런싱 가능)
    - DB 스토리지를 공유하기 때문에 병목현상이 발생 가능
    
    Active-StandBy
      - 한쪽은 대기 상태로 두어 서버 하나가 다운되면 대기 상태 서버를 올리는 방식
      - FailOver가 이루어지는 동안 손실 발생
   ```
