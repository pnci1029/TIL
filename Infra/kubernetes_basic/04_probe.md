`probe의 목적`
```
  쿠버네티스에서 probe는 파드와 컨테이너 간 상태를 점검하는 매우 중요한 역할을 한다.

  startupProbe, readinessProbe, livenessProbe 세 가지 유형으로 나누어서 사용하며,
  각각의 종류는 다른 기능을 한다.
```
<br />
<br />

`예시`
```
      startupProbe:
        httpGet:
          path: "/startup"
          port: 8080
        periodSeconds: 5
        failureThreshold: 24
      readinessProbe:
        httpGet:
          path: "/readiness"
          port: 8080
        periodSeconds: 10
        failureThreshold: 3
      livenessProbe:
        httpGet:
          path: "/liveness"
          port: 8080
        periodSeconds: 10
        failureThreshold: 3
```

`startupProbe`
```
  앱 초기화가 완료되었는지 체크하는 API

  앱이 처음 실행되었을때 쿠버네티스에서 startupProbe에 정의된 API에
  정의된 주기로 요청을 보내서 앱 초기화가 완료되었는지 확인한다.

  완료가 된 후, 쿠버네티스는
  startupProbe를 중지시키고

  readinessProbe와 livenessProbe를 동작시킨다.
```

- <img width="1480" alt="스크린샷 2024-06-16 오후 3 16 03" src="https://github.com/pnci1029/TIL/assets/81909140/243ea2c2-39b8-4b27-8e7e-394ca0692a8b">
  - probe들이 앱 초기화와 실행에 따라서 false에서 true로 변화는 모습을 확인할 수 있다.

- <img width="1463" alt="스크린샷 2024-06-16 오후 2 59 16" src="https://github.com/pnci1029/TIL/assets/81909140/ae56951b-fb9e-4081-8af7-ac0e01c903ad">


<br />


`readinessProbe`

<br />
<br />
<br />
<br />
<br />
출처 (https://www.inflearn.com/course/lecture?courseSlug=%EC%BF%A0%EB%B2%84%EB%84%A4%ED%8B%B0%EC%8A%A4-%EC%96%B4%EB%82%98%EB%8D%94-%ED%81%B4%EB%9E%98%EC%8A%A4-%EC%A7%80%EC%83%81%ED%8E%B8-sprint1&unitId=205452&tab=curriculum)
