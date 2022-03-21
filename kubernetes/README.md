## MiniKube

```shell
minikube config set cpus 6
minikube config set memory 7959

sudo minikube tunnel
minikube dashboard
```

## 从私有仓库拉取镜像

[从私有仓库拉取镜像](https://kubernetes.io/zh/docs/tasks/configure-pod-container/pull-image-private-registry/)

```shell
kubectl create secret docker-registry dockerhub-aliyun \
  --docker-server=registry.cn-shenzhen.aliyuncs.com \
  --docker-username=no.today@outlook.com \
  --docker-password=xxx \
  --docker-email=no.today@outlook.com
```

## References

- [kubectl 备忘单](https://kubernetes.io/zh/docs/reference/kubectl/cheatsheet/)
- [Kubectl Reference Docs](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)
- [Helm | 快速入门指南](https://helm.sh/zh/docs/intro/quickstart/)