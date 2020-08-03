## Setup first kubernetes master node

Now you are ready to run install command.

```
 $ kubeadm init --control-plane-endpoint api.kct.mylab.local:6443 --pod-network-cidr=10.244.0.0/16  --upload-certs
```

Here in above i am using endpoint as my haproxy load balancer VIP dns name, therefore as expected api interface will be the loadbalancer vip for all kubernetes nodes and environment.

Now once you get success msg configure your context on node 1 master.

```
$  mkdir -p $HOME/.kube
$  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$  sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Now you can run kubectl commands.

Next we will add all other new control plane node in to this.


[Read me](README.md)
