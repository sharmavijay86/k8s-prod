## Join worker nodes into kubernetes cluster

The control plane join command was generated already during [first master node setup](first-master.md) 

and the sametime worker node join command also generated, hence we will be using that command to join two worker nodes.


```
kubeadm join api.kct.mylab.local:6443 --token bhfce9.9m9dom27p40ftiwv \
    --discovery-token-ca-cert-hash sha256:5eb646d6729c353dca56063425d2b9b769097efef9184d147922b193a7878aad 

```

Here in above i am using again endpoint as my haproxy load balancer VIP dns name, therefore as expected api interface will be the loadbalancer vip for all kubernetes nodes and environment.

Now once you get success msg you can check the nodes from any of master node using kubectl command.

```
$ kubectl get node
NAME                STATUS   ROLES    AGE     VERSION
kctl1.mylab.local   Ready    master   7h48m   v1.18.6
kctl2.mylab.local   Ready    master   7h38m   v1.18.6
kctl3.mylab.local   Ready    master   7h37m   v1.18.6
kwrk1.mylab.local   Ready    <none>   7h13m   v1.18.6
kwrk2.mylab.local   Ready    <none>   7h12m   v1.18.6

```

[Read me](README.md)
