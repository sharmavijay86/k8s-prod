## Setting up CNI plugin on first master node 

same step applicable for single node cluster as well

Now when you have already setup your [first master node](first-master.md) 

We can use any of cni plugin. But i am in my setup using calico tigera operator method install.

1. Install the Tigera Calico operator and custom resource definitions.

```  $ kubectl create -f https://docs.projectcalico.org/manifests/tigera-operator.yaml  ```

2. Install Calico by creating the necessary custom resource. You may need to change the default IP pool CIDR to match your pod network CIDR before running the setup manifests hence get the manifest download 

``` $ wget https://docs.projectcalico.org/manifests/custom-resources.yaml ```

Now edit cidr to meet as per your pod cidr given during first master node setup.

Now apply config manifest.

``` $ kubectl apply -f custom-resources.yaml ```

3. Confirm that all of the pods are running with the following command.

```$  watch kubectl get pods -n calico-system ```

Done!


Instead of calico if you wish to use weavnet, simply apply manifest as bellow:

```
$ kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')" 
```

Done!

if you want to setup CNI other than calico  do bellow.
### weave net cni
```
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
```

### flannel CNI
```
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```
[Read me](README.md)
