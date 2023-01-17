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
  - 계층구조(layer)
  - <img width="1649" alt="스크린샷 2023-01-14 오후 1 00 20" src="https://user-images.githubusercontent.com/81909140/212449801-8561573b-9663-4070-9492-5f8f566b32c3.png">
    - docker image inspect ubuntu 
  - <img width="1285" alt="스크린샷 2023-01-14 오후 1 00 58" src="https://user-images.githubusercontent.com/81909140/212449813-8fb1968d-ade1-47ec-818d-b1f323aa9573.png">
  - 레이어들은 해시값으로 저장되어있음

  
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
  
  컨테이너는 호스트 서버에서 각자의 프로세스로 실행됨
  -> 각 컨테이너는 개별 네트워크망을 가진다(서로 다른 ip)
  host <-> 컨테이너 (bridge를 통해 네트워킹) 컨테이너 <-> 컨테이너?
  ```  
  #  
  - <img width="642" alt="스크린샷 2023-01-12 오후 9 57 05" src="https://user-images.githubusercontent.com/81909140/212072319-6e91d386-ce52-4bb8-8e89-a2b50ce6e472.png">
  - Host
    - eth0 : 호스트 서버에서 사용하고 있는 private IP 값
    - docker0 : 도커 데몬에 의해 생성되는 기본 bridge network, 호스트의 eth0과 컨테이너의 veth 사이를 연결해주는 브릿지 역할
  - Container
    - eth0 : 호스트와 연결하기 위한 컨테이너의 ip 값
    - veth : 가상 eth로, 컨테이너의 eth 생성과 함께 브릿지 네트워크와 연결하기 위해 생성되는 가상 eth  
#  
#  
# 도커 볼륨과 바인드 마운트
```
  도커늩 컨테이너마다 독립된 저장소를 가지고 있다.
  컨테이너가 종료될 시 컨테이너 내부의 데이터들도 함께 사라진다.
  데이터의 영속성을 보장하기 위해 볼륨과 바인드 마운트를 이용한다.
  볼륨과 바인드 마운트는 컨테이너와 파일시스템을 분리하여 관리한다.
  컨테이너를 지웠다가 다시 실행해도 도커 볼륨과 연결한다면 데이터는 그대로 유지된다
```
  - 볼륨
    - 도커 엔진이 관리하는 도커 내부 스토리지 디렉토리에 새 디렉토리를 생성하여 컨테이너 내부의 볼륨 데이터를 저장하는 방식
    - 생성된 볼륨은 자동으로 호스트의 도커 스토리지 디렉토리인 /var/lib/docker/volumes/~ 에 저장된다
    - 해당 볼륨을 컨테이너에 탑재하면 위 디렉토리가 컨테이너에 탑재되며, 도커에 의해 관리되며 호스트 시스템의 핵심 기능과 분리된다?>???
    - 바인드 마운트가 호스트 머신의 디렉토리 구조나 OS에 의존적인 반면, 볼륨은 도커에 의해 완전히 관리된다. 
#  
#
#
## 도커 이미지 - 파일 명령어
  ```
  # node-js server   -> # + ~~ 주석처리
  FROM node:16       -> FROM 지시어를 통해 도커파일 실행 베이스 이미지 지시(node:16)
  LABEL maintainer simple/docker -> LABLE 빌드하는 이미지의 메타데이터 값. 옵셔널값
  
  WORKDIR /app.      -> working directory 경로 지정 (리눅스 cd 와 같다고 이해)
  ```



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
    - docker run -d --name my-test -nginx -> 백그라운드에 my-test란 이름의 nginx 컨테이너 실행
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

