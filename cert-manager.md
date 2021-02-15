## Automatic certificate provisioner for kubernetes

Apply manifest from jetstack

```
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v0.16.0/cert-manager.yaml
```
Create a cluster issuer for self signed certificates.

```
vim  selfsighned-issuer.yaml

apiVersion: cert-manager.io/v1alpha2
kind: ClusterIssuer
metadata:
  name: selfsigned-issuer
  namespace: default
spec:
  selfSigned: {}

```
Apply the manifets

```  
kubectl apply -f selfsighned-issuer.yaml
```

Now you can create ingress rule by giving referance of this cluster issuer in annotation field. example bellow.

```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
    annotations:
      kubernetes.io/ingress.class: nginx
      cert-manager.io/issuer: "selfsigned-issuer"
    name: nginx-test
    namespace: default
spec:
    rules:
      - host: nginx1.apps.kct.mylab.local
        http:
          paths:
            - backend:
                serviceName: nginxnew
                servicePort: 80
              path: /
    tls:
        - hosts:
            - nginx1.apps.kct.mylab.local
          secretName: nginx-cert-tls
```
Only this annotation with cluster issuer will create a certificate for you as per name given in secret here. e.g above nginx-cert-tls
if you will run command to verify 

```
kubectl get certificate -n default
NAME             READY   SECRET           AGE
nginx-cert-tls   True    nginx-cert-tls   3m22s

```

in order to configure letsencrypt certificate and if you are running k8s on public cloud.

add certificate issuer as 

```
apiVersion: cert-manager.io/v1alpha2
kind: ClusterIssuer
metadata:
  name: letsencrypt-staging
spec:
  acme:
    # You must replace this email address with your own.
    email: user@example.com
    server: https://acme-staging-v02.api.letsencrypt.org/directory
    privateKeySecretRef:
      # Secret resource that will be used to store the account's private key.
      name: example-issuer-account-key
    # Add a single challenge solver, HTTP01 using nginx
    solvers:
    - http01:
        ingress:
          class: nginx
```

[Read me](README.md)
