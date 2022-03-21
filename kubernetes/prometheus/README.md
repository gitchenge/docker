```shell
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm upgrade --install prometheus prometheus-community/kube-prometheus-stack -f values.yaml \
  --namespace prometheus --create-namespace

kubectl apply -f ingress.yaml
```

admin/prom-operator

## References

- [Prometheus and Grafana installation](https://kubernetes.github.io/ingress-nginx/user-guide/monitoring/#prometheus-and-grafana-installation)
- [Grafana NGINX Ingress controller](https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/grafana/dashboards/nginx.json)