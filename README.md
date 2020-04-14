# DevOps-Kubernetes

## Namespaces

- Wordpress
- Mysql
- Prometheus
- Grafana
- kubeAPIServer (pour google auth)

## Liens:
https://hub.docker.com/_/wordpress

https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/

# Commandes:
> kubectl apply -f config.yml  
> kubectl port-forward pod/wordpress 8080:80

# RBAC:

Create Services accounts:
```
> kubectl apply -f  serviceAccount.yaml
```

Create Roles:
```
> kubectl apply -f  clusterRole.yaml
```

Binding services accounts to users:
```
> kubectl apply -f  clusterRoleBinding.yaml
```

Get the token of a special service account:
```
> kubectl get sa <user> -o yaml
```

Expected output:
```
apiVersion: v1
kind: ServiceAccount
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"ServiceAccount","metadata":{"annotations":{},"name":"<user>","namespace":"default"}}
  creationTimestamp: "2020-04-13T15:21:01Z"
  name: <user>
  namespace: default
  resourceVersion: "222038"
  selfLink: /api/v1/namespaces/default/serviceaccounts/<user>
  uid: 512d253a-11a3-4d77-b77c-c8cff73793a7
secrets:
- name: <user>-token-srtcz #Here is the token
```

Get the access token to the api for a special service account:
```
> kubectl get secrets <user>-token-srtcz -o yaml
```

Expected output:
```
apiVersion: v1
data:
  ca.crt: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUM1ekNDQWMrZ0F3SUJBZ0lCQVRBTkJna3Foa2lHOXcwQkFRc0ZBREFWTVJNd0VRWURWUVFERXdwdGFXNXAKYTNWaVpVTkJNQjRYRFRFNU1USXhOakV6TXpFeU5Wb1hEVEk1TVRJeE5ERXpNekV5TlZvd0ZURVRNQkVHQTFVRQpBeE1LYldsdWFXdDFZbVZEUVRDQ0FTSXdEUVlKS29aSWh
2Y05BUUVCQlFBRGdnRVBBRENDQVFvQ2dnRUJBTU9kCjFZUkdsc2N2MzdEeFhVVE0yd21DN0l6WHVKcjdUU2xDbjdQTGlVaU5kYkdweVI4bmNvUDhKK1c1a3RCQ2JHTHYKcWlMbFlQeDl2bSt5UUxXN0lPQ3ZMbCswOWRvTEJ4dzlXYXd3V2t3LzdnQUIrek8zN281UUNtUjB2OEp4dkU3NwpQZGZDU3BnMzdKcUYwQjREMkNKeG1VYUhDRzU5MlJ5WTUwUmRz
aVNuSVB6d3ErclAreURmVTVHWVhORWlmcHhMClVRL2ZXQ0JyVCtJQm9SWG5FWVdBUjZIdEVRSkdsOGdpRElVMHhMOGd0ajF2OWM4eCtWaDFTQVM1Y2p1V0F6djMKOGNWTmk0cmQ5TDVFWDRyUU1kVTJ0cXlKblVMeXJha2pLQXorQlJjeUI0bHBRakNOWFNNQTNCMWZQRG0veFBxTgpIdlg4WU5talEvNjZYWkVlZHlzQ0F3RUFBYU5DTUVBd0RnWURWUjBQQ
VFIL0JBUURBZ0trTUIwR0ExVWRKUVFXCk1CUUdDQ3NHQVFVRkJ3TUNCZ2dyQmdFRkJRY0RBVEFQQmdOVkhSTUJBZjhFQlRBREFRSC9NQTBHQ1NxR1NJYjMKRFFFQkN3VUFBNElCQVFDSHR0TWM4enlFdzVBa3U5SHhJc25HZ3ZySE1SY0RIcE1CUEcyZ3NwSjhuUWpBQjNKbQozazRESXI3aEppTlNTcEFpRDltNTRiRFhTTitObkt0azUvVmlyaHpsNTNBS3
ErSTFVNGxmWis2dnc2bEZoNEtsCjZ2S1NiT3R0emtic3VOTkNGeVlNTlB1RklIUTJPOFErVlp2Ky85LzR0eVZMVmEzSjJqSTFsSEFzbG5RRVphakcKc0Z4T3RkK1Mvbm4rODkyMitab2ptTStNam43YWlPSGthZHNobE5xVGl1dFVlMjl3TE94ajJzd29PWktmcnFiRwpwYTI5V29TYjhPUWZDdkpKWmlXQythQk1sNWk4N2FqaUF2VmFOd01YK1pmZXd3Smd
PaE5sK01XSFpzYVJxT1JaCnBPejVtSlhUUURGdU5tVTYvWVB6ak1ZaXpzSEx2NXhvdmpRRAotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCg==
  namespace: ZGVmYXVsdA==
  token: ZXlKaGJHY2lPaUpTVXpJMU5pSXNJbXRwWkNJNkluZFNWMFV4WW5WbFZ6bG5jVEJEYjNJelV6ZGZRM0JoUWsxUFlXUTJjVFJVV0VKbWEwdElhMlZKYTI4aWZRLmV5SnBjM01pT2lKcmRXSmxjbTVsZEdWekwzTmxjblpwWTJWaFkyTnZkVzUwSWl3aWEzVmlaWEp1WlhSbGN5NXBieTl6WlhKMmFXTmxZV05qYjNWdWRDOXVZVzFsYzNCaFkyVWlP
aUprWldaaGRXeDBJaXdpYTNWaVpYSnVaWFJsY3k1cGJ5OXpaWEoyYVdObFlXTmpiM1Z1ZEM5elpXTnlaWFF1Ym1GdFpTSTZJbUpsYm05cGVHUmxiV0ZqWVdSaGJXbGhMWFJ2YTJWdUxYTnlkR042SWl3aWEzVmlaWEp1WlhSbGN5NXBieTl6WlhKMmFXTmxZV05qYjNWdWRDOXpaWEoyYVdObExXRmpZMjkxYm5RdWJtRnRaU0k2SW1KbGJtOXBlR1JsYldGa
llXUmhiV2xoSWl3aWEzVmlaWEp1WlhSbGN5NXBieTl6WlhKMmFXTmxZV05qYjNWdWRDOXpaWEoyYVdObExXRmpZMjkxYm5RdWRXbGtJam9pTlRFeVpESTFNMkV0TVRGaE15MDBaRGMzTFdJM04yTXRZemhqWm1ZM016YzVNMkUzSWl3aWMzVmlJam9pYzNsemRHVnRPbk5sY25acFkyVmhZMk52ZFc1ME9tUmxabUYxYkhRNlltVnViMmw0WkdWdFlXTmhaR0
Z0YVdFaWZRLk50Rko1Nm1mTGJUMnZlS3BlSnNVUG1qVWNndWxJYzhkTTBzZTRlT0hDTXNMRVE5cEZRLThJd1NySS1wYWFRaUJta1g5ZTh2WTRHcjNENk1DRDlhbnpoTlo4dHY2cERGNDdiNmNWMW9CR2JQbjl3LU5LTTZhM3lZR1MzMmJzSThlQUNEUTc4RG9ZQkRzUWc5WUFWanh4eWo5VzJzYkdBc2E5X3M5cTNpaV9fSlJ0bDZhUGdRZExlT0tJMm9QSWJ
6ekg1a2VOcEFjUWhKdjdMM0IzNjJENW5uZmNnLXpfNFBFbmMyejFnRV93aUZ2cjI3R0hxSDAwWGxacHljYjZ6LVVKenFnVnJYVEc0VVRRZlFsWmp0OUZFTG80cWxYU25FQlhfcWo1SWo2d00wZUM0VFV4YVFiWmxmZ1VxVDh0dkw2M1pjREFTcGVyZkdUVVJmSnpGWHB6dw==
kind: Secret
metadata:
  annotations:
    kubernetes.io/service-account.name: benoixdemacadamia
    kubernetes.io/service-account.uid: 512d253a-11a3-4d77-b77c-c8cff73793a7
  creationTimestamp: "2020-04-13T15:21:01Z"
  name: benoixdemacadamia-token-srtcz
  namespace: default
  resourceVersion: "222037"
  selfLink: /api/v1/namespaces/default/secrets/benoixdemacadamia-token-srtcz
  uid: a6d74d59-6891-44e6-98e4-71b5b074ac52
type: kubernetes.io/service-account-token
```

Before doing that you have to go in the minikube dashboard (by using the cmd "minikube dashboard") and get the name of the mysql pods or the wordpress pods to get the name of one of them to verify the permissions
Check if everything is working:
```
> kubectl exec -ti <pod-name> -- sh #go in the pod terminal
> apt update && apt upgrade
> apt install curl
> cat /run/secrets/kubernetes.io/serviceaccount/<name-of-a-user-mount/token #get the token of the user you asked for
> TOKEN=$(cat /run/secrets/kubernetes.io/serviceaccount/<name-of-a-user-mount/token) #set the token in a env variable
> curl -H "Authorization: Bearer $TOKEN" https://kubernetes/api/v1/ --insecure #test the connection to the api
> curl -H "Authorization: Bearer $TOKEN" https://kubernetes/api/v1/<resource-name> --insecure #if you get the result that means you have the perms to see it, if not, you don't have the right perms to see
```

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

