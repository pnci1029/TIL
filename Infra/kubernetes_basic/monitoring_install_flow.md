`모니터링 도구 설치 전 파드 상황`
- <img width="754" alt="스크린샷 2024-04-22 오후 7 47 38" src="https://github.com/pnci1029/TIL/assets/81909140/bf1b6f7a-684c-4e4e-950e-5b269d386b64">
<br/>
<br/>


`1. 깃허브를 통해 프로메테우스, 그라파나, 로키 yaml 설치`
```
  [root@k8s-master ~]# yum -y install git

  # 로컬 저장소 생성
git init monitoring
git config --global init.defaultBranch main
cd monitoring

  # remote 추가 ([root@k8s-master monitoring]#)
git remote add -f origin https://github.com/k8s-1pro/install.git

  # sparse checkout 설정
git config core.sparseCheckout true
echo "ground/k8s-1.27/prometheus-2.44.0" >> .git/info/sparse-checkout
echo "ground/k8s-1.27/loki-stack-2.6.1" >> .git/info/sparse-checkout

# 다운로드 
git pull origin main
```

<br />
<br />

`3. 프로메테우스 설치`
```
  # 설치 ([root@k8s-master monitoring]#)
kubectl apply --server-side -f ground/k8s-1.27/prometheus-2.44.0/manifests/setup
kubectl wait --for condition=Established --all CustomResourceDefinition --namespace=monitoring
kubectl apply -f ground/k8s-1.27/prometheus-2.44.0/manifests

  # 설치 확인 ([root@k8s-master]#) 
kubectl get pods -n monitoring
```

<br />
<br />

`4. 로키 설치`
```
  # 설치 ([root@k8s-master monitoring]#)
kubectl apply -f ground/k8s-1.27/loki-stack-2.6.1
  
  # 설치 확인
kubectl get pods -n loki-stack
```
  
- <img width="817" alt="스크린샷 2024-04-22 오후 7 49 17" src="https://github.com/pnci1029/TIL/assets/81909140/2e99db6e-7965-419a-afb0-0548c07d5c79">

<br />
<br />
`5. 설치 대시보드 확인`
```
  1. http://192.168.56.30:30001/ 초기 id/pw : admin/admin

  2. 쿠버네티스 대시보드를 통해 샘플 앱 파드 생성
    https://192.168.56.30:30000/ -> 우측상단 + 클릭

    yaml 값 입력 후 적용

```
  - <img width="1065" alt="스크린샷 2024-04-27 오후 2 34 58" src="https://github.com/pnci1029/TIL/assets/81909140/8227c9e2-5756-4a74-b59e-48e2a8501364">

```
  3.
```
   
  

<br />
<br />
<br />
<br />
<br />
<br />
(출처 : https://www.inflearn.com/course/lecture?courseSlug=%EC%BF%A0%EB%B2%84%EB%84%A4%ED%8B%B0%EC%8A%A4-%EC%96%B4%EB%82%98%EB%8D%94-%ED%81%B4%EB%9E%98%EC%8A%A4-%EC%A7%80%EC%83%81%ED%8E%B8-sprint1&unitId=205433)

