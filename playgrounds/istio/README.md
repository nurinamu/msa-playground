# istio 놀이터

각종 istio 관련 기능들을 올려보고 사용해봅니다.

## 서비스 메쉬올리기

### minikube에 첫 istio 설치 시도

아래 명령을 통해서 현재 kubectl에 연결된 context에 istio 설치 시도
```
$ istioctl install // 현재 k8s cluster에 istio 설치
```

> 결과는 타임아웃.. [stackoverflow](https://stackoverflow.com/questions/64373346/istioctl-install-fails-with-multiple-timeouts)의 이야기에 따르면 리소스 부족이라고 한다. 

local에서 잡아둔 minikube에 할당된 리소스가 작은 것이 1차적 문제고, 2차적으로는 istioctl install시 기본 profile로 설치되는 것들의 리소스가 할당된 것보다 커서 인데. 1차적 문제는 내가 맥을 바꾸지 전까지 더 리소스를 올려주기는 어려워서 최소로 필요한 istio 리소스 체크를 위해서 2차적 이슈를 최적화 먼저하고 1차 이슈를 체크하는 걸로 접근해보자.

### istioctl install profile 리소스 손보기

TBD