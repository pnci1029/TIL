`컨테이너 기반 앱 생성 과정`
- <img width="405" alt="스크린샷 2024-04-20 오후 2 13 28" src="https://github.com/pnci1029/TIL/assets/81909140/a83a55b6-8808-403b-be4f-6e2f8a21b116">

`컨테이너 오케스트레이션 앱 생성 과정`
- <img width="392" alt="스크린샷 2024-04-20 오후 2 13 32" src="https://github.com/pnci1029/TIL/assets/81909140/4b156cc4-337a-4279-b29d-fe628e042767">

```

  쿠버네티스 = 컨테이너 오케스트레이션으로 동의어로 생각을 할 수 있으나
  사실 다른 오케스트레이션도 많다.

  그러나 쿠버네티스의 점유율이 워낙 높기 때문에 동의어로 보였을뿐

  아래 이미지 참고
```
- <img width="1159" alt="스크린샷 2024-04-20 오후 2 20 49" src="https://github.com/pnci1029/TIL/assets/81909140/982bf7bc-f143-4f30-b89d-8eb3bb8066c4">

#  
$  
```

  현재 컨테이너 오케스트레이션 도구는 쿠버네티스가 주류가 되었으나

  컨테이너 도구 간 경쟁이 심해지고 있다.

  도커 컨테이너 기술의 주류였지만
  쿠버네티스와의 호환성에 문제가 있었고,

  쿠버네티스간의 호환성이 현재 컨테이너 기술 선택의 큰 결정요소가 되었다.

  또 다른 컨테이너들 중
  contaiderd와 cri-o가 있는데
  containerd는 도커에서 분리가 되어 나왔다.


  containderd는 클라우드 기술의 표준을 관장하는 CNCF(Cloud Native Computing Foundation)를 줄업했다고 나오는데

  클라우드 기술 선택 시 CNCF를 졸업했다고 하면 믿고 쓰면 된다.

  아래 이미지 참고
```
  - <img width="1614" alt="스크린샷 2024-04-20 오후 2 31 44" src="https://github.com/pnci1029/TIL/assets/81909140/330d6950-71dc-4629-af87-b96af6035dbe">
#  
 
`컨테이너를 도커에서 dockerd로 바꾸게 되면 도커로 만들어둔 이미지를 새로 만들어야할까?`
```
  도커도 dockerd를 사용하여 컨테이너를 만들기 때문에 결국 만들어지는 컨테이너는 같다.
  따라서 이미지를 새로 만들 필요는 없다.
```

#  
#  
#  
#  
#  
#  
#  
(출처 https://www.inflearn.com/course/lecture?courseSlug=%EC%BF%A0%EB%B2%84%EB%84%A4%ED%8B%B0%EC%8A%A4-%EC%96%B4%EB%82%98%EB%8D%94-%ED%81%B4%EB%9E%98%EC%8A%A4-%EC%A7%80%EC%83%81%ED%8E%B8-sprint1&unitId=177374)

