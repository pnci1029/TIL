# Gradle 을 이용한 빌드
  ```
  1. Gradle 설치
    ~> brew install gradle (+gradle --version)
  2. gradle init --dsl=groovy--type=java-application--test-framework=junit--package=com.test--project-name=test-docker-spring-boot 프로젝트 생성
  3. 구조확인 tree
  ```
  - <img width="1033" alt="스크린샷 2023-05-15 오후 9 58 41" src="https://github.com/pnci1029/TIL/assets/81909140/cc29b309-10fd-4f75-86e2-724a83232e90">
  #  
  #  
  ```
  App.java 경로 접근
  ```
  - <img width="1009" alt="스크린샷 2023-05-15 오후 10 04 16" src="https://github.com/pnci1029/TIL/assets/81909140/61a8d8fb-c1cd-4669-b8c2-a4de360f2e7e">

  #  
  ```
  연습예제
  프로젝트 jar 파일 빌드
   gradle build --info
    jar 파일 생성
  ```
  - <img width="793" alt="스크린샷 2023-05-15 오후 10 10 11" src="https://github.com/pnci1029/TIL/assets/81909140/547e748a-decb-44cc-9765-478c1f7be4ef">

  #  
  ```
  포크 뜬 도커파일이 있는 프로젝트 빌드를 위해 도커 셋업
  1. docker login
    (DockerFile)
    아래 이미지 경로에 접근 
    
  2. 해당 프로젝트 gradle 빌드
  gradle build --info
    2.1 build 디렉토리 생성되었는지 확인
    2.2 build/libs/.jar 파일 생성 확인
  
  3. 도커 빌드
  docker build -t dockerId/test:1.0 ./
  3.1 docker images -> respository 생성 확인
  
  4. 도커 푸시
  docker push dockerId/test:1.0
  ```
  - <img width="374" alt="스크린샷 2023-05-15 오후 10 19 00" src="https://github.com/pnci1029/TIL/assets/81909140/e9354c95-5479-4257-bcb3-5960a925941a">

  
