# Elastic Cloud on Kubernetes (ECK)

> https://github.com/elastic/cloud-on-k8s

[Operator pattern](https://kubernetes.io/ko/docs/concepts/extend-kubernetes/operator/) 을 통해 Elastic 제품군을 관리합니다.

Prepare Local Kubernetes Cluster
```zsh
$ kubectl config use-context minikube
$ minikube addons enable ingress
```

Follow below commands step by step.
> Caution: CPU/Memory 가 아주 많이 필요합니다.
```zsh
$ kubectl apply -n elastic-system -f 1_eck.yaml
# kubectl logs -n elastic-system -f statefulset.apps/elastic-operator

$ kubectl apply -n elastic-system -f 2_elasticsearch.yaml
# PASSWORD=$(kubectl get secret quickstart-es-elastic-user -o go-template='{{.data.elastic | base64decode}}')

$ kubectl apply -n elastic-system -f 3_kibana.yaml
# USER=elastic
# PASSWORD=$(kubectl get secret quickstart-es-elastic-user -o=jsonpath='{.data.elastic}' | base64 --decode)

$ kubectl apply -n elastic-system -f 4_apm.yaml
# APM_TOKEN=$(kubectl get secret/apm-server-quickstart-apm-token -o go-template='{{index .data "secret-token" | base64decode}}')
```

Kibana dashboard 를 expose 하는 방법을 [링크](https://www.elastic.co/guide/en/cloud-on-k8s/current/k8s-tls-certificates.html)를 통해 확인할 수 있습니다.


Clean resources.
```zsh
$ kubectl delete -n elastic-system -f 4_apm.yaml && \
  kubectl delete -n elastic-system -f 3_kibana.yaml && \
  kubectl delete -n elastic-system -f 2_elasticsearch.yaml && \
  kubectl delete -n elastic-system -f 1_eck.yaml
```

And,
* Metricbeat
  * https://www.elastic.co/kr/infrastructure-monitoring
  * https://www.elastic.co/guide/en/beats/metricbeat/current/running-on-kubernetes.html#running-on-kubernetes
* APM
  * https://www.elastic.co/guide/en/apm/get-started/current/index.html
  * APM agents: https://www.elastic.co/guide/en/apm/get-started/current/agents.html
  * OpenTracing: https://www.elastic.co/guide/en/apm/get-started/current/opentracing.html
