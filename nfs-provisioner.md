## NFS dynamic storage provisioner for kubernetes

Install packages on all worker nodes .

```
yum install nfs-utils -y
```
You should have already install and configured helm, if not then check metrics server install section.

Create a new namespace for storage

```
kubectl create ns app-storage

```

Deploy package. you should replace your server name ip and export dir path.

```
helm install nfs --set nfs.server=192.168.1.73,nfs.path=/srv/nfs/kubedata,storageClass.defaultClass=true stable/nfs-client-provisioner -n app-storage
```
Done!

You can check storage class

```
kubectl get sc
NAME                   PROVISIONER                                RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
nfs-client (default)   cluster.local/nfs-nfs-client-provisioner   Delete          Immediate           true                   0h08m

```


[Read me](README.md)
