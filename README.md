# DevOps-Kubernetes

## Namespaces

- kubeDB
- Wordpress
- Apache
- Prometheus
- Grafana
- kubeAPIServer (pour google auth)

## Liens:
https://hub.docker.com/_/wordpress

# Commandes:
> kubectl apply -f config.yml  
> kubectl port-forward pod/wordpress 8080:80

# Wordpress:

Install: 
```
> kubectl apply -k ./
> minikube service wordpress --url
```
Delete:
```
> kubectl delete -k ./
```
