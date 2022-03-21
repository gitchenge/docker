```shell
helm upgrade --install elasticsearch elastic/elasticsearch -f ./elasticsearch/values.yaml \
  --namespace elk --create-namespace

helm upgrade --install kibana elastic/kibana -f ./kibana/values.yaml \
  --namespace elk --create-namespace

helm install metricbeat elastic/metricbeat --namespace elk

helm upgrade --install fluentd bitnami/fluentd -f ./fluentd/values.yaml \
  --namespace elk --create-namespace
```

[Deployment Fluentd](https://docs.dapr.io/zh-hans/operations/monitoring/logging/fluentd/)
[Fluentd Document](https://docs.fluentd.org/)