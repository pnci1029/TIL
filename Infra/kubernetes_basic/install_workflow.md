`모든 설치전 준비사항`
```
  1. 호환되는 리눅스 머신. 쿠버네티스 프로젝트는 데비안 기반 배포판, 레드햇 기반 배포판
  2. 2 GB 이상의 램을 장착한 머신. (이 보다 작으면 사용자의 앱을 위한 공간이 거의 남지 않음
  3. 2 이상의 CPU
  4. 스왑의 비활성화 (뭔지모르겠음)

      상세 : https://kubernetes.io/ko/docs/setup/production-environment/tools/kubeadm/install-kubeadm/
```

<br />

`쿠버네티스 설치`
```
  1. 컨테이너 런타임 설치

    detail (
        파드에서 컨테이너를 실행하기 위해, 쿠버네티스는 컨테이너 런타임을 사용,
        컨테이너 런타임이 여러 개 감지되거나 하나도 감지되지 않은 경우, kubeadm은 에러를 반환하고 사용자가 어떤 것을 사용할지를 명시하도록 요청
        )

    1-1 컨테이너 런타임 설치전 사전세팅
      1.1 iptables 세팅
          cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
          overlay
          br_netfilter
          EOF
          
          sudo modprobe overlay
          sudo modprobe br_netfilter
          
          # 필요한 sysctl 파라미터를 설정하면, 재부팅 후에도 값이 유지된다.
          cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
          net.bridge.bridge-nf-call-iptables  = 1
          net.bridge.bridge-nf-call-ip6tables = 1
          net.ipv4.ip_forward                 = 1
          EOF
          
          # 재부팅하지 않고 sysctl 파라미터 적용하기
          sudo sysctl --system

      1.2 컨테이너 런타임(containderd 설치)

      1.3 cri 활성화


  2. kubeadm, kubelet 및 kubectl 설치
        

      상세 : https://kubernetes.io/ko/docs/setup/production-environment/container-runtimes/
```

<br />

`마스터 노드 세팅`
```
  1. kubeadm으로 클러스터 생성
    1.1 클러스터 초기화
    1.2 kubectl 사용 설정
    1.3 CNI 플러그인 설치
    1.4 matser 에 파드 생성할 수 있도록 설정
```



#  
#  
#  
#  
#  
(출처 : https://www.inflearn.com/course/lecture?courseSlug=%EC%BF%A0%EB%B2%84%EB%84%A4%ED%8B%B0%EC%8A%A4-%EC%96%B4%EB%82%98%EB%8D%94-%ED%81%B4%EB%9E%98%EC%8A%A4-%EC%A7%80%EC%83%81%ED%8E%B8-sprint1&unitId=205416,
https://kubernetes.io/ko/docs/setup/production-environment/tools/kubeadm/install-kubeadm/
)
