# keycloak-kubernetes

with this repo you can install keycloak on kubernetes. 



## postgres sts

first create db user and password

```
kubectl create secret generic keycloak-db-secret --from-literal=username="your-username" --from-literal=password="your-password"
```

you need to install postgres as a statefullset. before that you need create persistenvolume. clone this repo 

```
kubectl apply -f keycloak-kubernetes/db/.
```

## keycloak operator

first you need keycloak kubernetes operator

```
kubectl apply -f https://raw.githubusercontent.com/keycloak/keycloak-k8s-resources/24.0.2/kubernetes/keycloaks.k8s.keycloak.org-v1.yml
kubectl apply -f https://raw.githubusercontent.com/keycloak/keycloak-k8s-resources/24.0.2/kubernetes/keycloakrealmimports.k8s.keycloak.org-v1.yml

kubectl apply -f https://raw.githubusercontent.com/keycloak/keycloak-k8s-resources/24.0.2/kubernetes/kubernetes.yml
```

## keycloak app

before you need generate a self signed certificate or apply your own certificate if you have already one.

you can genereta certificate like this;

```
openssl req -subj '/CN=keycloak.yourdomain.com/O=Test Keycloak./C=US' -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

```
kubectl create secret tls keycloak-tls --cert certificate.pem --key key.pem
```

then install keycloak.yaml

```
kubectl apply -f keycloak-kubernetes/keycloak/.
```

## admin

last action is create dns record or add dns name your hostname with kubernetes loadbalancer IP then access gui with below user and password

```
kubectl get secret keycloak-initial-admin -o jsonpath='{.data.username}' | base64 --decode
kubectl get secret keycloak-initial-admin -o jsonpath='{.data.password}' | base64 --decode
```

