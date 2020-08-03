## NFS server setup on Centos 7

Install package.

```
yum install nfs-utils -y
```

disable selinux

```
sed -i ‘s/^SELINUX=enforcing$/SELINUX=permissive/’ /etc/selinux/config
```

disable firewalld  or configure for nfs and rpcbind
```
systemctl stop firewalld && systemctl disable firewalld
```
create a directory for kubernetes export

```
mkdir /srv/nfs/kubedata -p
```
create the export 
```
vim /etc/exports

/srv/nfs/kubedata	192.168.1.0/24(sync,rw,no_root_squash)
```
save exit

Now enable and restart services

```
systemctl enable nfs-server && systemctl start nfs-server
systemctl enable rpcbind && systemctl start rpcbind
```
[Read me](README.md)
