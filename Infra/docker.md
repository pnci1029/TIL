# Docker ?
  - 하드웨어 / 호스트 OS(window, MacOS...) / Docker Contaier(Host OS)
    - 컨테이너는 Host OS 기준 Process에 해당 
  - 컨테이너 엔진 중 하나
  - 

# 도커 이미지와 컨테이너
  ## 이미지
  - 이미지와 컨테이너는 1:N 관계
  - 이미지는 컨테이너를 실행시키기 위해 필요한 요소
  - 각 컨테이너에 목적에 맞는 바이너리와 의존성이 설치되어있음
  - 계층구조 
  
#
  ## 컨테이너
  - 호스트와 다른 컨테이너들로부터 **격리**되어있음
  - 프로세스
  - 이미지를 읽기전용으로 사용
  - 컨테이너에서 무슨짓을 하더라도 이미지에 영향 X  
#  
#
  
  ## 이미지와 컨테이너
<img width="1052" alt="스크린샷 2023-01-03 오전 12 04 25" src="https://user-images.githubusercontent.com/81909140/210248957-f87de212-dc12-48d2-8388-f84d68bd0d28.png">



  
#  
#  
# 도커 명령어
  - * 아래 명령어 수행 시 이미지가 없을경우 먼저 pull 받고 해당 명령어 수행 
  - docker create [image]   -> 이미지 생성
  - docker run [image]      -> 생성 및 시작
  - docker start [image]    -> 시작
  - docker create [image]  
#
  - docker ps               -> 프로세스중인 컨테이너 조회
  - docker ps -a            -> 전체 컨테이너 조회
  - docker inspect [container] -> 컨테이너 내부정보 조회
#  
#
+  쿠버네티스 환경구축을위한 셋업
- brew install kubectl
- brew install kustomize
- brew install minikube + minikube start --driver docker
