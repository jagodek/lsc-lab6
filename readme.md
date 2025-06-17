
# Requirements
Install docker desktop\
Install kubectl\
Install kind\
Install helm


# Commands
## 1. Create kubernetes cluster:
```
kind create cluster
```
Cluster is group of kubernetes nodes. Nodes can be individual hardware units or virtual machines.

## 2. Install chart with custom name of storageClass.
```
$ helm repo add nfs-ganesha-server-and-external-provisioner https://kubernetes-sigs.github.io/nfs-ganesha-server-and-external-provisioner/
$ helm install my-release nfs-ganesha-server-and-external-provisioner/nfs-server-provisioner --set=storageClass.name=default
```
This will create pod of nfs-server-provisioner.

## 3. Create PersistentVolumeClaim
```
kubectl apply -f my-pvclaim.yml
```
Persistent volume claim is request from user for using storage in node. It defines size of claim and access mode.

You can confirm it works with
```
kubectl get pvc
```

```example
NAME         STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   VOLUMEATTRIBUTESCLASS   AGE
my-pvclaim   Bound    pvc-8646eddb-4b03-46ef-b293-a6eaa6ffc019   100Mi      RWO            default        <unset>                 53s
```


## 4. Apply deployment. 
```
kubectl apply -f my-deployment.yml
```
Deployment manages set of pods running app. It defines number of replicas in pod

## 5. Start service
```
kubectl apply -f my-service.yml 
```
Service exposes application to single outward endpoint.

Verify it by:
```
kubectl get pods -l app=nginx-app
```



## 6. Create mapping to index.html
```
kubectl create configmap web-content-configmap --from-file=index.html
```

## 7. Create job
```
kubectl apply -f my-job.yml 
```


## 8. Create port forwarding. In new console launch 
```
kubectl port-forward service/my-service 8080:80
```

## 9. Verification
Run
```
curl http://localhost:8080
```