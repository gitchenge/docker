## Quick start

```shell
kubectl create namespace jenkins
kubectl apply -f pv.yaml
kubectl apply -f pvc.yaml
```

```shell
minikube ssh
sudo chown 1000:1000 /data/jenkins_home/
```

```shell
helm repo add jenkins https://charts.jenkins.io
helm upgrade --install jenkins jenkins/jenkins -f values.yaml \
  --namespace jenkins --create-namespace
```

```shell
kubectl create clusterrolebinding jenkins --clusterrole cluster-admin --serviceaccount=jenkins:default
```

[kubectl create clusterrolebinding](https://kubernetes.io/zh/docs/reference/access-authn-authz/rbac/#kubectl-create-clusterrolebinding)

## References

- [Helm Repo](https://artifacthub.io/packages/helm/jenkinsci/jenkins#install-chart)
- [Jenkins pipeline syntax(declarative)](https://www.jenkins.io/doc/book/pipeline/syntax/#declarative-directives)
- [Kubernetes plugin for Jenkins](https://plugins.jenkins.io/kubernetes/#plugin-content-declarative-pipeline)
- [Kubernetes plugin examples](https://stackoverflow.com/a/62445227/12679246)