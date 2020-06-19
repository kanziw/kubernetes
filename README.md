# kubernetes

> Kubernetes playground using [minikube](https://github.com/kubernetes/minikube)  
> minikube 를 이용하여 local 에 kuberenets(이하 k8s)를 구성, k8s 를 연습합니다.  

## Installation

Install minikube
```zsh
$ brew install minikube
```

Install kubectl
```zsh
$ brew install kubernetes-cli
```

## Kubernetes cluster

```zsh
$ minikube start \
    --keep-context \
    --kubernetes-version=v1.18.3 \
    --disk-size='10g'
```

* --keep-context : This will keep the existing kubectl context and will create a minikube context.
* --kubernetes-version=v1.18.3 : 2020.06.15 기준 최신의 k8s version.
* --disk-size='10g'

```zsh
$ kubectl config use-context minikube
```

## Other tools

여러 k8s cluster 를 운영 중이라면 [kube-ps1](https://github.com/jonmosco/kube-ps1) & [kubectx](https://github.com/ahmetb/kubectx) 를 설치하여 사용하는 것을 강력하게 추천합니다.

```zsh
$ brew install kube-ps1 kubectx
```
