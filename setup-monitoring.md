## Setup monitoring of kubernetes cluster using Prometheus, node-exporter and grafana.

We will be using prometheus operator  to setup monitoring

Create a namespace

``` 
kubectl create ns monitoring
```
get the values of helm chart

```
helm inspect values stable/prometheus-operator > /tmp/values.yaml
```
edit to modify values

```
vim /tmp/values.yaml
```

edit bellow values in prometheus.prometheusSpec.storageSpec section

```
   storageSpec:
      volumeClaimTemplate:
        spec:
          accessModes: ["ReadWriteOnce"]
          resources:
            requests:
              storage: 10Gi
```
			  
save and exit.

now apply helm 

```
helm install prometheus stable/prometheus-operator \
--set prometheus.ingress.enabled=true \
--set prometheus.ingress.hosts[0]=prometheus.apps.kct.mylab.local \
--set prometheus.ingress.annotations."cert-manager\.io/cluster-issuer"=selfsigned-issuer \
--set alertmanager.ingress.enabled=true \
--set alertmanager.ingress.hosts[0]=alertmanager.apps.kct.mylab.local \
--set alertmanager.ingress.annotations."cert-manager\.io/cluster-issuer"=selfsigned-issuer \
--set grafana.ingress.enabled=true \
--set grafana.ingress.hosts[0]=grafana.apps.kct.mylab.local \
--set grafana.ingress.annotations."cert-manager\.io/cluster-issuer"=selfsigned-issuer \
--values /tmp/values.yaml \
--namespace monitoring
```

in your case please replace cert-manager clusterissuer and for sure hostnames of ingress.




[Read me](README.md)
