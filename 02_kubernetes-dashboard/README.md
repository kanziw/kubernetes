# dashboard

> https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/

fyi)
* Local dashboard 이기에 kubernetes-dashboard user 에게 cluster-admin 권한을 binding 하였다.
* auth check 를 skip 한다.

```zsh
$ kubectl apply -f kubernetes-dashboard.yaml
$ kubectl proxy
Starting to serve on 127.0.0.1:8001
```

Visit `http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/` and press `skip`
