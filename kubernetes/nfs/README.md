## Install nfs server `ubuntu`

### Server

```shell
sudo apt install nfs-kernel-server nfs-common
sudo mkdir -p /data/nfs

sudo vim /etc/exports
/data/nfs *(ro,sync,insecure,no_root_squash,no_subtree_check)

sudo exportfs -a
sudo service nfs-kernel-server restart
```

### Mac mount nfs

```shell
sudo mount -o nolock -t nfs [IP]:/data/nfs /private/nfs
```

本地挂载没问题再用K8s挂

## Deployment on k8s

执行命令稍微给点间隔时间

```shell
kubectl create namespace nfs
kubectl apply -f pv.yaml
kubectl apply -f pvc.yaml
kubectl apply -f nginx.yaml
kubectl expose deployment nginx -n nfs
kubectl create ingress ingress-local --class=nginx --rule="localhost/*=nginx:80" -n nfs
curl http://localhost
```

## References

- [配置 Pod 以使用 PersistentVolume 作为存储](https://kubernetes.io/zh/docs/tasks/configure-pod-container/configure-persistent-volume-storage/)