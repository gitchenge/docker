## Quick start


1. Deploy nginx-ingress and wait ready

```shell
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm upgrade --install ingress-nginx ingress-nginx/ingress-nginx -f values.yaml \
  --namespace ingress-nginx --create-namespace
```

```shell

kubectl get pods --namespace=ingress-nginx

kubectl wait --namespace ingress-nginx \
  --for=condition=ready pod \
  --selector=app.kubernetes.io/component=controller \
  --timeout=120s
```

2. Deploy httpd and expose service

```shell
kubectl create deployment httpd --image=httpd --port=80 -n httpd
kubectl expose deployment httpd -n httpd
```

3. Config ingress-proxy

```shell
kubectl create ingress ingress-local --class=nginx --rule="localhost/*=httpd:80" -n httpd
kubectl get ingress ingress-local -o yaml -n httpd
```

4. CURL

```shell
curl http://localhost
```

5. Destroy httpd after check

```shell
kubectl delete namespace httpd
```

## References

- [Helm Repo](https://artifacthub.io/packages/helm/ingress-nginx/ingress-nginx)
- [Installation Guide](https://kubernetes.github.io/ingress-nginx/deploy/)