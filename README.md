# kuberntes-dashboard
## Uninstall

1. Remove metrics server resources:


```bash
kubectl delete -f ./kubernetes/kubernetes-dashboard/metrics-server-components.yaml
```
2. Remove `k8s` dashboard resources:

```bash
kubectl delete -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.5.0/aio/deploy/recommended.yaml
```

## Install

1. Create metric server resources to enable `top` example: `kubectl top pod -A`

```bash
kubectl apply -f ./metrics-server-components.yaml
```

2. Create kubernetes dashboard resources

    -  Check latest version of kubernetes dashboard [here](https://github.com/kubernetes/dashboard/releases)

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.5.0/aio/deploy/recommended.yaml
```

3. Review all resources created in namespace

```bash
kubectl get all -n kubernetes-dashboard
```

4. Configure admin user

```bash
kubectl apply -f ./admin-user.yaml
```

```bash
kubectl apply -f ./admin-user2.yaml
```

1. Get admin user token (old version)

```bash
kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret |grep admin-user-token | awk '{print $1}')
```

6. Get admin user token (new versions)

```bash
kubectl -n kubernetes-dashboard create token admin-user
```

6. Run kubernetes proxy

```bash
kubectl proxy
```

And access kubernetes dashboard with the following link: http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login
