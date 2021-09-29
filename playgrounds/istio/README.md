# istio 놀이터

각종 istio 관련 기능들을 올려보고 사용해봅니다.

## 서비스 메쉬올리기

### minikube에 첫 istio 설치 시도

istioctl install로 설치되는 [profile 설정표](https://istio.io/latest/docs/setup/additional-setup/config-profiles/)를 확인하면 default profile로 설치시 istiod와 istio-ingressgateway가 설치된다고 한다.

```
$ istioctl install // 현재 k8s cluster에 istio 설치
```

결과는 아래와 같은 메세지를 출력하면서 끝난다.

```
✔ Istio core installed                                                                                                    
✘ Istiod encountered an error: failed to wait for resource: resources not ready after 5m0s: timed out waiting for the condition
  
✘ Ingress gateways encountered an error: failed to wait for resource: resources not ready after 5m0s: timed out waiting for the condition
  Deployment/istio-system/istio-ingressgateway (container failed to start: ContainerCreating: )
- Pruning removed resources   
```

일단 kubectl에서 보이는 istio-ingressgateway 애러 메세지를 보니 이렇다.

```
message: '0/1 nodes are available: 1 Insufficient memory.'
```

> req 메모리가 얼마나 필요한가?

우선 istiod가 pending되어 있어 pod의 yaml을 찍어보니 기본 req resource가 cpu:500m / memory:2Gi 다.

내가 띄운 minikube가 기본 docker 드라이버로 띄우게 되어있어 mac docker desktop에 설정된 리소스 안에서 설정된다. docker desktop resource를 보니 메모리가 2Gi로 잡혀있어 이걸 일단 4Gi로 올려보자.

```
✔ Istio core installed          
✔ Istiod installed                                    
✔ Ingress gateways installed                                    
✔ Installation complete 
```

`성공`

아직 instagram clone 서비스를 만들기 전이기 떄문에 [gcp msa demo](https://github.com/GoogleCloudPlatform/microservices-demo)를 올려보자. 근데 다 올릴려니 리소스가 부족해서 istio-proxy가 제대로 올라오는지만 보기위해 [frontend](https://github.com/GoogleCloudPlatform/microservices-demo/blob/master/release/kubernetes-manifests.yaml) 하나만 올려보자.

올려보면
```
frontend-dcb95b78d-5mmnw 1/1 Running 0 31s
```

서비스 container만 떠있고 기대했던 istio-proxy container가 주입이 안되어있다.

[istio 문서](https://istio.io/latest/docs/setup/additional-setup/sidecar-injection/)를 참조해보면 `istio-injection=enabled`를 namespace label로 지정해야 자동으로 주입된다고 한다.

```
$ kubectl label ns default istio-injection=enabled --overwrite
```

이제 frontend pod을 죽여서 새로 생성해보자.

```
frontend-dcb95b78d-kn5x5 2/2 Running 0 47s
```

`진짜 이제 기본 설치 끝`