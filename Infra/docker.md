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
# 
  
  ## 이미지와 컨테이너
<img width="1052" alt="스크린샷 2023-01-03 오전 12 04 25" src="https://user-images.githubusercontent.com/81909140/210248957-f87de212-dc12-48d2-8388-f84d68bd0d28.png">. 
#
#

# 도커 엔트리포인트와 커맨드?
  - 엔트리포인트
    - 도커 컨테이너가 실행될때 기본적으로 실행하는 스크립트나 명령어
    - 생략이 가능하고 생략할경우 커맨드에 지정된 명령어 수행
      - ex) ubuntu 경우 /bash.  
    - 기본 명령어 수행 시(docker run ubuntu)
      - <img width="1591" alt="스크린샷 2023-01-07 오후 1 29 35" src="https://user-images.githubusercontent.com/81909140/211131602-5803a70e-25ce-49a4-a6c2-dcb95101d40b.png">
      - <img width="550" alt="스크린샷 2023-01-07 오후 1 30 04" src="https://user-images.githubusercontent.com/81909140/211131608-ec97a6c7-e21d-498b-b5fe-2ee687db4116.png">
    - 엔트리포인트 지정 + 커스텀 네이밍 지정 실행 시(docker run --entrypoint sh --name test-ubuntu ubuntu)
      - <img width="1546" alt="스크린샷 2023-01-07 오후 1 33 01" src="https://user-images.githubusercontent.com/81909140/211131639-271a7712-fa81-4a9b-887c-2831c1f9efed.png">
      -  <img width="307" alt="스크린샷 2023-01-07 오후 1 33 19" src="https://user-images.githubusercontent.com/81909140/211131655-c4fedf4b-91d2-42bf-8b1e-a7db17cf4fde.png">
#  
#  
# 도커 exec
  - 실행중인 도커 컨테이너에 명령어를 실행 (docker exec [contaier] [명령어])


# 도커 네트워크
  ```
  도커 컨테이너는 격리된 환경에서 동작하기때문에 다른 컨테이너와 통신이 불가능하다.
  하지만 다른 컨테이너와 네트워크 연결을 통해 통신이 가능하게 사용할 수 있다.
  ```


  
#  
#  
# 도커 명령어
  - * 아래 명령어 수행 시 이미지가 없을경우 먼저 pull 받고 해당 명령어 수행 
  - docker create [image]   -> 이미지 생성
  - docker run [image]      -> 생성 및 시작
  - docker start [image]    -> 시작
  - docker create [image]  
#
  - docker ps -> 프로세스중인 컨테이너 조회
  - docker ps -a -> 전체 컨테이너 조회(프로세스중 + 프로세스 종료)
  - docker inspect [container] -> 컨테이너 내부정보 상세정보 조회
  - docker -i -t -> 기본 커맨드 실행 (ubuntu 처럼 실행 시 바로 종료될때 사용??)
  - ctrl + p + q -> 종료하지않고 명령어 입력
  - docker run -d [container] -> docker run [container]로 실행하면 foreground로 바로 실행되지만, 데몬(d)로 실행 시 백그라운드로 실행
    - ps로 검색 시 조회되며 다른명령어 실행 가능
    - docker run -d --name my-test -nginx -> 백그라운드에 my-test란 이름의 nginx 이미지 실행
  - docker run -p 80(호스트 포트):80(컨테이너 포트) nginx -> nginx 포트번호가 80이라 컨테이너포트에 80 기입
    - curl localhost:80 을 통해 80번 호스트 포트에 nginx 실행확인


#  
#
+  쿠버네티스 환경구축을위한 셋업
- brew install kubectl
- brew install kustomize
- brew install minikube + minikube start --driver docker. 
#. 
#  
#
  - docker exec [container] [command]    ->  
#. 
#  
#
도커 이미지 리소스
https://hub.docker.com/_/nginx

