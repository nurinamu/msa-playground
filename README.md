# msa-playground

MSA 관련 기술들을 이것저것 돌려보는 놀이터용 레포입니다.
(제가 맥이기 때문에 모든 것은 맥기준.)

## 최소요구사항

- [k8s](https://kubernetes.io/) 환경을 기본으로 하기 때문에 k8s 환경을 가지고 있거나 로컬에 [minikube](https://minikube.sigs.k8s.io/docs/start/) 를 설치하여야 합니다.

- [kubectl](https://kubernetes.io/ko/docs/tasks/tools/install-kubectl-macos/)을 설치 해야합니다.

- [istioctl](https://istio.io/latest/docs/reference/commands/istioctl/)을 사용하기 위해 [istio](https://istio.io/)를 다운 받아야합니다.

## 놀이터에서 작업할 내용들

- [instagram clone web 서비스](https://github.com/nurinamu/msa-playground/tree/main/playgrounds/msa)
    - webfront + (apigw) + apiserver + db + (cache)
    - 모두 k8s cluster 안에 구축
- [k8s 연습](https://github.com/nurinamu/msa-playground/tree/main/playgrounds/k8s)
    - 클러스터 이중화 연습
    - 내부망 / 외부망 접근제어 연습
    - [kustomize](https://kustomize.io/) 각종 기능들 연습
- [istio 연습](https://github.com/nurinamu/msa-playground/tree/main/playgrounds/istio)
    - monitoring 관련 설정 ( [prometheus](https://prometheus.io/) + [grafana](https://grafana.com/) )
- [CI / CD 연습](https://github.com/nurinamu/msa-playground/tree/main/playgrounds/ci-cd)
    - [github action](https://docs.github.com/en/actions)을 통한 ci/cd
    - [jenkins](https://www.jenkins.io/) + [argocd](https://argoproj.github.io/argo-cd/)를 통한 ci/cd

## 기본 실행환경

``` sh
$ minikube start // minikube 실행
$ kubectl config use-context minikube // minikube context로 연결
```
