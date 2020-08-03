## Setting up metallb load balancer for baremetal kubernetes servioce load balancer.

Lets first enable ARP in your kubeproxy so that it can add new NAT rules for load balancer services.

```
kubectl get configmap kube-proxy -n kube-system -o yaml | sed -e "s/strictARP: false/strictARP: true/" | kubectl apply -f - -n kube-system
```
Now apply manifests to create namespace and deployments.

```
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.3/manifests/namespace.yaml
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.3/manifests/metallb.yaml
kubectl create secret generic -n metallb-system memberlist --from-literal=secretkey="$(openssl rand -base64 128)"
```

create a config map with range of ip allocated for LB use.

```
vim iplb-cm.yaml
```

put contents like bellow replace ip range as per your cluster setup

```
apiVersion: v1
kind: ConfigMap
metadata:
  namespace: metallb-system
  name: config
data:
  config: |
    address-pools:
    - name: default
      protocol: layer2
      addresses:
      - 192.168.1.240-192.168.1.250
```
Now apply this config map 

```	  
kubectl apply -f iplb-cm.yaml
```

Done!

you can test this with a sample nginx deployment and then exposing as load balancer type service.

```
kubectl create deployment nginx --image=nginx

kubectl expose deployment nginx --port=80 --type=LoadBalancevc
NAME         TYPE           CLUSTER-IP    EXTERNAL-IP     PORT(S)        AGE
kubernetes   ClusterIP      10.96.0.1     <none>          443/TCP        8h
nginx        LoadBalancer   10.98.66.67   192.168.1.241   80:30110/TCP   74s
```

See nginx service get one external ip just like in aws ELB IP.


[Read me](README.md)
