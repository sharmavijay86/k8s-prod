## Join other control plane kubernetes master nodes

The control plane join command was generated already during [first master node setup](first-master.md) 

we will further use that command to join other two nodes as master.

```
  kubeadm join api.kct.mylab.local:6443 --token bhfce9.9m9dom27p40ftiwv \
    --discovery-token-ca-cert-hash sha256:5eb646d6729c353dca56063425d2b9b769097efef9184d147922b193a7878aad \
    --control-plane --certificate-key a4abe46db1b705b036f2e4034158b54427eeb779b5a4a00af0ff44c6ef350e14
```

Here in above i am using again endpoint as my haproxy load balancer VIP dns name, therefore as expected api interface will be the loadbalancer vip for all kubernetes nodes and environment.

Now once you get success msg configure your context on both other masters.

```
$  mkdir -p $HOME/.kube
$  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$  sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Now you can run kubectl commands.

Using same above defined method you can add / join other control plane nodes.


[Read me](README.md)
