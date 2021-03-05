## Setup metrics in kubernetes cluster.

We will be doing almost all steps with helm so if you dont have helm client use bellow method to get it setup first.

```
$ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
$ chmod 700 get_helm.sh
$ ./get_helm.sh
```
or 

```
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```
Now before moving to install metrics-server in kubernetes lets add first google stable helm repo.

Add helm repo

```
$ helm repo add stable https://kubernetes-charts.storage.googleapis.com
```

search metrics-server helm chart

```
$ helm search repo metrics-server
NAME                 	CHART VERSION	APP VERSION	DESCRIPTION                                       
stable/metrics-server	2.11.1       	0.3.6      	Metrics Server is a cluster-wide aggregator of ...
```

inspect chart values to alter them

``` $ helm inspect values stable/metrics-server > /tmp/metrics-server.values ```

edit values as bellow-


``` $ vim /tmp/metrics-server.values
```

in hostnetwork:

set

``` enabled: true```

and in

args:

uncomment

```
args:
- --kubelet-insecure-tls
```

save and exit. Now create namespace and install metrics server.

```
$ kubectl create ns metrics

$ helm install metrics-server stable/metrics-server --namespace metrics --values /tmp/metrics-server.values

```
you can list anytime .

```
$ helm ls -n metrics
```

now you will be able to run top command to check resource usage as bellow-

```
$ kubectl top node
NAME                CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%   
kctl1.mylab.local   409m         20%    1861Mi          50%       
kctl2.mylab.local   335m         16%    1546Mi          41%       
kctl3.mylab.local   322m         16%    1530Mi          41%       
kwrk1.mylab.local   277m         13%    3395Mi          22%       
kwrk2.mylab.local   229m         11%    3095Mi          20%   
```
Done !

[Read me](README.md)
