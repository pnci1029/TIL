# Object
1. Master node - 디렉토리 생성


`Namespace`
```
- Object들을 그룹핑 해주는 역할



apiVersion: v1
kind: Namespace
metadata:
  name: anotherclass-123
  labels:
    part-of: k8s-anotherclass
    managed-by: dashboard
```
<br />
<br />

`Deployment`
```
- 파드를 만들고 업그레이드 시키는 공간
- 여기에 네임스페이스로 위에 만든 이름을 사용하게 되면 해당 네임스페이스를 따르는 deployment가 된다.

* 동일한 네임스페이스 내에서 Deployment는 중복이 되어서는 안된다.


apiVersion: apps/v1
kind: Deployment
metadata:
  namespace: anotherclass-123
  name: api-tester-1231
  labels:
    part-of: k8s-anotherclass
    component: backend-server
    name: api-tester
    instance: api-tester-1231
    version: 1.0.0
    managed-by: dashboard
spec:
  selector:
    matchLabels:
      part-of: k8s-anotherclass
      component: backend-server
      name: api-tester
      instance: api-tester-1231
  replicas: 2                             // ------------> 중요
  strategy:
    type: RollingUpdate                   // ------------> 매우 중요
  template:                     // ------------> 파드를 띄울 실제 정보들을 포함
    metadata:
      labels:
        part-of: k8s-anotherclass
        component: backend-server
        name: api-tester
        instance: api-tester-1231
        version: 1.0.0
    spec:
      nodeSelector:                   // ------------> 파드를 띄울 노드 선택
        kubernetes.io/hostname: k8s-master
      containers:
        - name: api-tester-1231
          image: 1pro/api-tester:v1.0.0        // ------------> 도커허브에 올라와있는 이미지 정보
          ports:
          - name: http
            containerPort: 8080
          envFrom:                       // ------------> 어플리케이션의 환경변수 
            - configMapRef:
                name: api-tester-1231-properties
          startupProbe:        // ------------> 앱이 정상 기동되었는지 확인 재기동 or 아래 probe 가동
            httpGet:
              path: "/startup"
              port: 8080
            periodSeconds: 5
            failureThreshold: 24
          readinessProbe:                   // ------------> 앱의 트래픽 연결 속성
            httpGet:
              path: "/readiness"
              port: 8080
            periodSeconds: 10
            failureThreshold: 3
          livenessProbe:                   // ------------> 앱이 비정상이면 재시동할건지 설정
            httpGet:
              path: "/liveness"
              port: 8080
            periodSeconds: 10
            failureThreshold: 3
          resources: // --------> 파드에 CPU/메모리 맥시멈 설정(미설정시 파드가 노드의 모든 자원을 써버리게된다.)
            requests:
              memory: "100Mi"
              cpu: "100m"
            limits:
              memory: "200Mi"
              cpu: "200m"
          volumeMounts:
            - name: files
              mountPath: /usr/src/myapp/files/dev
            - name: secret-datasource
              mountPath: /usr/src/myapp/datasource
      volumes:
        - name: files
          persistentVolumeClaim:
            claimName: api-tester-1231-files
        - name: secret-datasource
          secret:
            secretName: api-tester-1231-postgresql


```

<br />
<br />

`Service`
```
- 파드에 트래픽을 연결시켜주는 역할

apiVersion: v1
kind: Service
metadata:
  namespace: anotherclass-123                  // ------------> 여전히 위 네임스페이스 이름 사용
  name: api-tester-1231
  labels:
    part-of: k8s-anotherclass
    component: backend-server
    name: api-tester
    instance: api-tester-1231
    version: 1.0.0
    managed-by: dashboard
spec:
  selector:
    part-of: k8s-anotherclass
    component: backend-server
    name: api-tester
    instance: api-tester-1231
  ports:
    - port: 80
      targetPort: http
      nodePort: 31231
  type: NodePort
```

<br />
<br />

`Configmap, Secret`
```
- 파드에 환경변수 값을 제공


apiVersion: v1
kind: ConfigMap
metadata:
  namespace: anotherclass-123
  name: api-tester-1231-properties
  labels:
    part-of: k8s-anotherclass
    component: backend-server
    name: api-tester
    instance: api-tester-1231
    version: 1.0.0
    managed-by: dashboard
data:
  spring_profiles_active: "dev"
  application_role: "ALL"
  postgresql_filepath: "/usr/src/myapp/datasource/postgresql-info.yaml"
---
apiVersion: v1
kind: Secret
metadata:
  namespace: anotherclass-123
  name: api-tester-1231-postgresql
  labels:
    part-of: k8s-anotherclass
    component: backend-server
    name: api-tester
    instance: api-tester-1231
    version: 1.0.0
    managed-by: dashboard
stringData:
  postgresql-info.yaml: |
    driver-class-name: "org.postgresql.Driver"
    url: "jdbc:postgresql://postgresql:5431"
    username: "dev"
    password: "dev123"
```

<br />
<br />

`PVC, PV`
```
- PV 는 Namespace 정보가 없다.
- 이는 PV Object가 클러스터 레벨의 Object이기 때문(나머지는 Namespce레벨의 Object)
  * PersistentVolume, Namespace는 클러스터 레벨  Deployment, Service들은 Namespace 레벨
- 

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  namespace: anotherclass-123
  name: api-tester-1231-files
  labels:
    part-of: k8s-anotherclass
    component: backend-server
    name: api-tester
    instance: api-tester-1231
    version: 1.0.0
    managed-by: kubectl
spec:
  resources:
    requests:
      storage: 2G
  accessModes:
    - ReadWriteMany
  selector:
    matchLabels:
      part-of: k8s-anotherclass
      component: backend-server
      name: api-tester
      instance: api-tester-1231-files
---
apiVersion: v1
kind: PersistentVolume
metadata:
  name: api-tester-1231-files
  labels:
    part-of: k8s-anotherclass
    component: backend-server
    name: api-tester
    instance: api-tester-1231-files
    version: 1.0.0
    managed-by: dashboard
spec:
  capacity:
    storage: 2G
  volumeMode: Filesystem
  accessModes:
    - ReadWriteMany
  local:
    path: "/root/k8s-local-volume/1231"
  nodeAffinity:
    required:
      nodeSelectorTerms:
        - matchExpressions:
            - {key: kubernetes.io/hostname, operator: In, values: [k8s-master]}
```

<br />
<br />

`HPA`
```
- 부하에 따라 파드를 늘리거나 줄이는 스케일링 역할


apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  namespace: anotherclass-123
  name: api-tester-1231-default
  labels:
    part-of: k8s-anotherclass
    component: backend-server
    name: api-tester
    instance: api-tester-1231
    version: 1.0.0
    managed-by: dashboard
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment               //-------------------> 스케일링 대상 지정(Deployment)
    name: api-tester-1231
  minReplicas: 2               //-------------------> 최소
  maxReplicas: 4               //-------------------> 최대
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 60               //-----------> 평균 40%가 늘어나면 스케일 아웃 설정
  behavior:
    scaleUp:
      stabilizationWindowSeconds: 120          //-----------> 파드 스케일 변화 후 지정 시간 후 재변환
```

<br />
<br />
<br />

```

파드들을 지우고 싶다면 네임스페이스를 지우면 내부의 Object들이 모두 삭제가됨
kubectl delete ns anotherclass-123

다만 PV는 네임스페이스 레벨이 아니기 때문에 별도 삭제 요청 필요
kubectl delete pv api-tester-1231-files

```



<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />


출처 (https://www.inflearn.com/course/lecture?courseSlug=%EC%BF%A0%EB%B2%84%EB%84%A4%ED%8B%B0%EC%8A%A4-%EC%96%B4%EB%82%98%EB%8D%94-%ED%81%B4%EB%9E%98%EC%8A%A4-%EC%A7%80%EC%83%81%ED%8E%B8-sprint1&unitId=162844,
https://cafe.naver.com/kubeops
)
