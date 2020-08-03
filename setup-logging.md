## Setup logging with Elasticsearch Kibana and FluentBit

We will be using manifests to deploy logging.

Clone this git repo

```
git clone https://github.com/sharmavijay86/k8s-prod.git

```

Now switch to es dir 

```
cd k8sprod/es
```
change your desired hostname in file 5-kibana-ingress.yaml

```
vim 5-kibana-ingress.yaml
```

save and exit! now run deploy.

```
kubectl apply -f ./
```

Done!



[Read me](README.md)
