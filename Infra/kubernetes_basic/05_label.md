`필요성`
```
  Cluster 레벨이든 NameSpace 레벨이든

  Object들은 메타데이터내에 라벨 정보들을 가지고 있다.
  Object들이 늘어남에 따라서 관리가 어려워질 수 있는데,

  라벨 관리가 잘 되어있으면 이런 문제들을 손쉽게 해결이 가능하다.
```
```
  labels:
    part-of: k8s-prometheus           // -> 어플리케이션 전체 이름
    component: prometheus             // -> 서비스를 구성하고 있는 각각의 구성 기능들
                                      // ex) part-of: k8s-prometues 하위 prometheus, grafana, exporter ...
    name: prometheus                  // -> 어플리케이션의 실제 이름
    instance: k8s                     // -> 인스턴스 식별 (쿠버네티스에 k8s-prometheus를 여러개 설치하는 상황이 생기는 경우에)
                                      // ex) instance: k8s-1, instance: k8s-2 등으로 인스턴스 분리하여 사용
    version: 2.44.0

```


<br />
<br />
<br />
<br />
<br />
출처 (https://www.inflearn.com/course/lecture?courseSlug=%EC%BF%A0%EB%B2%84%EB%84%A4%ED%8B%B0%EC%8A%A4-%EC%96%B4%EB%82%98%EB%8D%94-%ED%81%B4%EB%9E%98%EC%8A%A4-%EC%A7%80%EC%83%81%ED%8E%B8-sprint1&unitId=162844&tab=curriculum)
