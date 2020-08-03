## prepareing all kubernetes nodes

In this section we will be  preparing our all kubernetes nodes i.e. 3 master and 2 worker.

1. remove swap partition or use temporary

``` #sed -i '/swap/d' /etc/fstab
    # swapoff -a 
```
2. Disable firewalld service and selinux.

```
# systemctl disable firewalld
# systemctl stop firewalld
# setenforce 0 
# sed -i ‘s/^SELINUX=enforcing$/SELINUX=permissive/’ /etc/selinux/config
```

3. Now add kubernetes google repo

```
# cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
```

4. Install kubelet kubeadm kubectl and docker on nodes.

```
# yum install -y kubelet kubeadm kubectl docker
# systemctl enable kubelet && systemctl start kubelet
# systemctl enable docker && systemctl start docker

```
5. Add kernele parameters for network bridge  and apply changes.

```
# cat <<EOF > /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
```
```
# sysctl --system

```

6. Now prepull all required images into all nodes 

```bash

# kubeadm config images pull
# docker pull docker.io/calico/node:v3.15.1    
# docker pull docker.io/calico/pod2daemon-flexvol:v3.15.1
# docker pull docker.io/calico/cni:v3.15.1            
# docker pull docker.io/calico/kube-controllers:v3.15.1 
# docker pull docker.io/calico/typha:v3.15.1       
```

Done !


[Read me](README.md)
