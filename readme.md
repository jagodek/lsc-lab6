
# Requirements
Install docker desktop\
Install kubectl\
Install kind\
Install helm


# Commands
Create kubernetes cluster:
```
kind create cluster
```

Install chart with custom name of storageClass
```
$ helm repo add nfs-ganesha-server-and-external-provisioner https://kubernetes-sigs.github.io/nfs-ganesha-server-and-external-provisioner/
$ helm install my-release nfs-ganesha-server-and-external-provisioner/nfs-server-provisioner --set=storageClass.name=mystorage
```

Create PersistentVolumeClaim
```
kubectl apply -f pv-claim.yaml
```

You can confirm it works with
```
kubectl get pvc  test-dynamic-volume-claim
```

```
kubectl apply -f application/deployment.yaml
```

Start service
```
kubectl apply -f service.yml 
```

Verify it by:
```
kubectl get pods -l app=nginx
```


Create mapping to index.html
```
kubectl create configmap nginx-deployment --from-file=index.html=./index.html
```