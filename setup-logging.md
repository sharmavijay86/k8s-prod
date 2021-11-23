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
Now if we wish to test logs right after deployment, we can deploy a log generator app. Bellow is yaml

```YAML
# The Deployment which will run our log generator
apiVersion: apps/v1
kind: Deployment
metadata:
  name: random-generator
  namespace: random-generator
  labels:
    app: random-generator
spec:
  selector:
    matchLabels:
      app: random-generator
  template:
    metadata:
      labels:
        app: random-generator
    spec:
      containers:
      - name: random-generator
        imagePullPolicy: Always
        # You can build the image off the source code and push to your own docker hub if you prefer.
        image: chriscmsoft/random-generator:latest
```

Done!



[Read me](README.md)
