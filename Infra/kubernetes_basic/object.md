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
<br />
<br />
<br />
<br />
<br />
<br />


출처 (https://www.inflearn.com/course/lecture?courseSlug=%EC%BF%A0%EB%B2%84%EB%84%A4%ED%8B%B0%EC%8A%A4-%EC%96%B4%EB%82%98%EB%8D%94-%ED%81%B4%EB%9E%98%EC%8A%A4-%EC%A7%80%EC%83%81%ED%8E%B8-sprint1&unitId=162844,
https://cafe.naver.com/kubeops
)
