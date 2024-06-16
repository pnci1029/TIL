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
  1. http://192.168.56.30:30001/(그라파나) 초기 id/pw : admin/admin

  2. 쿠버네티스 대시보드를 통해 샘플 앱 파드 생성
    https://192.168.56.30:30000/ -> 우측상단 + 클릭

    yaml 값 입력 후 적용

```
- <img width="1712" alt="스크린샷 2024-04-27 오후 2 13 29" src="https://github.com/pnci1029/TIL/assets/81909140/de7461c4-e6e5-490e-9245-a233f192a622">
- <img width="1065" alt="스크린샷 2024-04-27 오후 2 34 58" src="https://github.com/pnci1029/TIL/assets/81909140/8227c9e2-5756-4a74-b59e-48e2a8501364">

```
  3. 그라파나 접속 후 샘플 파드 조회

```
<br />

- 파드정보
   - <img width="1697" alt="스크린샷 2024-04-27 오후 2 14 00" src="https://github.com/pnci1029/TIL/assets/81909140/fa5eb804-9494-4ec5-a4a7-63f127d586f1">
- 메트릭 정보
   - <img width="1710" alt="스크린샷 2024-04-27 오후 2 26 38" src="https://github.com/pnci1029/TIL/assets/81909140/271318e9-7497-4f04-abe0-714eba289128">

<br />
<br />


`샘플 앱 yaml 속성`
```
  apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-1-2-2-1
spec:
  selector:
    matchLabels:
      app: '1.2.2.1'
  replicas: 2          //---------> 파드 이중화 (Deploymnet -> replicas)
  strategy:
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: '1.2.2.1'
    spec:
      containers:
        - name: app-1-2-2-1
          image: 1pro/app
          imagePullPolicy: Always
          ports:
            - name: http
              containerPort: 8080
          startupProbe:
            httpGet:
              path: "/ready"
              port: http
            failureThreshold: 10
          livenessProbe:
            httpGet:
              path: "/ready"
              port: http
          readinessProbe:
            httpGet:
              path: "/ready"
              port: http
          resources:
            requests:
              memory: "100Mi"
              cpu: "100m"
            limits:
              memory: "200Mi"
              cpu: "200m"
---
apiVersion: v1
kind: Service           //---------> 기능 자체적으로 파드가 2개가 있을때 트래픽을 분산하여 처리
metadata:
  name: app-1-2-2-1
spec:
  selector:
    app: '1.2.2.1'
  ports:
    - port: 8080
      targetPort: 8080
      nodePort: 31221 //---> 마스터 노드에서 해당 포트로 트래픽을 보냈을때 이 앱에서 처리 (service -> replicas)
  type: NodePort
---
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: app-1-2-2-1
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: app-1-2-2-1
  minReplicas: 2          //---------> 스케일링 정보 미니멈 / 맥시멈
  maxReplicas: 4
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 40          //---------> 스케일링은 CPU가 평균 40% 초과했을때 증가 처리
```

<br />
<br />
<br />

`지속 트래픽 요청을 통해 스케일링 모니터링 확인`
```  
  while true; do curl http://192.168.56.30:31221/hostname; sleep 2; echo '';  done;
```
1. 두 파드에 번갈아가며 위 요청 처리
  - <img width="1116" alt="스크린샷 2024-04-27 오후 2 45 44" src="https://github.com/pnci1029/TIL/assets/81909140/f56d3929-f3f4-4e17-b9bb-f9d02bd4dff6">
2. 파드 두개 중 하나 삭제 (삭제 후 파드 재생성)
  - <img width="1466" alt="스크린샷 2024-04-27 오후 2 47 10" src="https://github.com/pnci1029/TIL/assets/81909140/43b3b9e9-09cc-4f80-9151-797654095dd6">
3. 삭제되자 남은 파드에 요청 후 재생성되자 다시 트래픽 분배
  - <img width="1311" alt="스크린샷 2024-04-27 오후 2 47 45" src="https://github.com/pnci1029/TIL/assets/81909140/836ad23e-640e-4988-9d6f-2849755fea1f">

  

<br />
<br />
<br />
<br />
<br />
<br />
(출처 : https://www.inflearn.com/course/lecture?courseSlug=%EC%BF%A0%EB%B2%84%EB%84%A4%ED%8B%B0%EC%8A%A4-%EC%96%B4%EB%82%98%EB%8D%94-%ED%81%B4%EB%9E%98%EC%8A%A4-%EC%A7%80%EC%83%81%ED%8E%B8-sprint1&unitId=205433, 
https://cafe.naver.com/kubeops)

