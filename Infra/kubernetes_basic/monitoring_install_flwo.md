`모니터링 도구 설치 전 파드 상황`
- <img width="754" alt="스크린샷 2024-04-22 오후 7 47 38" src="https://github.com/pnci1029/TIL/assets/81909140/bf1b6f7a-684c-4e4e-950e-5b269d386b64">
<br/>
<br/>


1. 깃허브를 통해 프로메테우스, 그라파나, 로키 yaml 설치
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
3. 프로메테우스 설치
```
  # 설치 ([root@k8s-master monitoring]#)
kubectl apply --server-side -f ground/k8s-1.27/prometheus-2.44.0/manifests/setup
kubectl wait --for condition=Established --all CustomResourceDefinition --namespace=monitoring
kubectl apply -f ground/k8s-1.27/prometheus-2.44.0/manifests

  # 설치 확인 ([root@k8s-master]#) 
kubectl get pods -n monitoring
```
4. 로키 설치
```
  # 설치 ([root@k8s-master monitoring]#)
kubectl apply -f ground/k8s-1.27/loki-stack-2.6.1
  
  # 설치 확인
kubectl get pods -n loki-stack
```
  
- <img width="817" alt="스크린샷 2024-04-22 오후 7 49 17" src="https://github.com/pnci1029/TIL/assets/81909140/2e99db6e-7965-419a-afb0-0548c07d5c79">



