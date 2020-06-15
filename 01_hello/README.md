# hello

Use default namespace
```zsh
$ kubens default
```

## Deploy a hello, world app
> https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/#deploy-a-hello-world-app

```zsh
$ minikube addons enable ingress

$ kubectl create deployment web --image=gcr.io/google-samples/hello-app:1.0
deployment.apps/web created

$ kubectl expose deployment web --type=NodePort --port=8080
service/web exposed

$ kubectl get service web
NAME   TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
web    NodePort   10.100.34.178   <none>        8080:32524/TCP   18s

$ minikube service web --url | xargs curl
Hello, world!
Version: 1.0.0
Hostname: web-6785d44d5-7qg2j
```

## Use ingress

```zsh
$ kubectl create deployment web2 --image=gcr.io/google-samples/hello-app:2.0
deployment.apps/web2 created

$ kubectl expose deployment web2 --port=8080 --type=NodePort
service/web2 exposed

$ kubectl apply -f example-ingress.yaml
ingress.networking.k8s.io/example-ingress created

$ ! (cat /etc/hosts | grep hello.kanziw.k8s) && \
    echo "$(minikube ip)\thello.kanziw.k8s" | sudo tee -a /etc/hosts
```

## Clean resources
```zsh
$ kubectl delete -f example-ingress.yaml
ingress.networking.k8s.io "example-ingress" deleted

$ kubectl delete service,deployment web2
service "web2" deleted
deployment.apps "web2" deleted

$ kubectl delete service,deployment web
service "web" deleted
deployment.apps "web" deleted

$ minikube addons disable ingress
🌑  "The 'ingress' addon is disabled
```
