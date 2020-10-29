![Kubernetes](images/k8slogo.png)
## How to setup a production ready kubernetes cluster?

A complete enterprise grade kubernetes production cluster setup.

#### Components

* Load Balancer setup with HAProxy and keepalived
* 3 node master setup with kubeadm
* 2 node worker setup with kubeadm
* ingress controller setup using nginx
* kubernetes service type load balancer setup using metallb
* kubernetes metrics setup
* kubernetes dynamic storage provisioning using nfs-provisioner
* kubernetes monitoring stack setup with prometheus operator
* kubernetes logging (ELK) setup elasticsearch,fluentbit and kibana
* helm setup deployments using helm
---
# Index

1. [Example lab setup used](setup-used.md)
1. [Load balancer setup](lb-setup.md)
1. [Prepration of all kubernetes nodes](prepare-nodes.md)
1. [Kubernetes first master node setup](first-master.md)
1. [Setup CNI Plugin](setup-cni.md)
1. [Add other master node into cluster](add-master.md)
1. [Add/join worker nodes into the cluster](add-workers.md)
1. [Setup metrics-server](add-metrics.md)
1. [Setup metallb - the baremetal k8s loadbalancer](add-metallb.md)
1. [NFS Server setup on separate Centos](nfs-server.md)
1. [setup nfs dynamic storage provisioner](nfs-provisioner.md)
1. [setup cert-manager](cert-manager.md)
1. [Setup nginx ingress controller](nginx-ingress.md)
1. [Setup monitoring with prometheus,node-exporter and grafana](setup-monitoring.md)
1. [Setup elastic search logging with kibana and fluentbit](setup-logging.md)
