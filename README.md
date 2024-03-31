# keycloak-kubernetes

with this repo you can install keycloak on kubernetes. 

## keycloak operator

first you need keycloak kubernetes operator

```
kubectl apply -f https://raw.githubusercontent.com/keycloak/keycloak-k8s-resources/24.0.2/kubernetes/keycloaks.k8s.keycloak.org-v1.yml
kubectl apply -f https://raw.githubusercontent.com/keycloak/keycloak-k8s-resources/24.0.2/kubernetes/keycloakrealmimports.k8s.keycloak.org-v1.yml

kubectl apply -f https://raw.githubusercontent.com/keycloak/keycloak-k8s-resources/24.0.2/kubernetes/kubernetes.yml
```

## postgres sts

you need to install postgres as a statefullset. before that you need create persistenvolume. clone this repo 

kubectl apply -f ./postgres/



