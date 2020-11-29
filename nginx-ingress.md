## Setup nginx as ingress controller

You should have already install and configured helm, if not then check metrics server install section.

Create a new namespace for storage

```
kubectl create ns ingress
```

Deploy package.

```
helm install nginx stable/nginx-ingress --set controller.metrics.enabled=true --namespace=ingress
```
An example Ingress that makes use of the controller:

I have given defined here annotation for self signed certificate from cert-manager. Hence this requires to setup cert-manager as per instruction in previous topic of cert-manager. then you will get generated certificate automatically.

```
  apiVersion: extensions/v1beta1
  kind: Ingress
  metadata:
    annotations:
      kubernetes.io/ingress.class: nginx
      cert-manager.io/issuer: "selfsigned-issuer"
    name: example
    namespace: foo
  spec:
    rules:
      - host: www.example.com
        http:
          paths:
            - backend:
                serviceName: exampleService
                servicePort: 80
              path: /
    tls:
        - hosts:
            - www.example.com
          secretName: example-tls
```

  
[Read me](README.md)
