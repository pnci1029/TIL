`전체 학습 워크플로우`
- <img width="1324" alt="스크린샷 2024-04-20 오후 3 18 01" src="https://github.com/pnci1029/TIL/assets/81909140/1926b926-53e3-46dc-af50-f3401c6d9da3">

#  
#  
#  
## 1. 인프라 환경 구축
#### 1.1 쿠버네티스 설치
```
  1. 가상 환경을 위한 virtual box 설치
    - Download : https://download.virtualbox.org/virtualbox/7.0.8/VirtualBox-7.0.8-156879-OSX.dmg

  2. Vagrant 설치
    - Download : https://releases.hashicorp.com/vagrant/2.3.4/vagrant_2.3.4_darwin_amd64.dmg

  //3. Vagrant 스크립트 수행 (private 내부)

  4. 가상환경 설정 세팅
    - Rocky 9.2와 UTM 연동하여 로컬 환경 세팅
      1. utm 환경 설정 실행
      2. rocky linux iso 파일 적용
      3. 호스트 PC에서 접속을 위한 네트워크, ip 주소 설정
      4. utm 설치 / 재설치 후 utm 재실행
      5. 호스트 PC에서 ssh 접속
      6. 쿠버네티스 설치 (arm 64)버전
      7. k get pods -A 설치 파드 확인
      8. 대시보드 확인 (https://할당 ip:30000/#/login)
    - 
```
