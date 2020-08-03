* Get the dns setup done 
* get the ntp sync with all node

--required url access need to be open directly 

- docker
- helm
- github

--dns setup and ip

---

|Node Type			|	IP Address   | Hostname |
|:--------------------------|:--------------------|:---------------------|
|haproxy load balancer node 	|	192.168.1.64 | lb1.mylab.local |
|haproxy load balancer node 	|	192.168.1.65 | lb2.mylab.local |
|keep alived virtual ip 	|	192.168.1.66 | api.kct.mylab.local |
|kubernetes  master node 1	|	192.168.1.68 | kctl1.mylab.local |
|kubernetes  master node 2	|	192.168.1.69 | kctl2.mylab.local |
|kubernetes  master node 3	|	192.168.1.70 | kctl3.mylab.local |
|kubernetes  worker node 1	|	192.168.1.71 | kwrk1.mylab.local |
|kubernetes  worker node 2	|	192.168.1.72 | kwrk2.mylab.local |
|nfs storage server node	|	192.168.1.73 | nfssrv.mylab.local |

---

[Read me](README.md)
