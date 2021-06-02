# shai-interv


Website:

Install Azure CLI:
```
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```
Connect to Azure CLI:
```
az login --identity
```
Install Kubernetes CLI:
```
sudo az aks install-cli
```
Connect to Kubernetes cluster on the Azure Cloud:
```
az aks get-credentials --resource-group devops-interview-rg --name shai-interview-aks --admin
```

Install the Nginx Ingress Controller:
```
kubectl create namespace ingress-basic

helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx

helm install nginx-ingress ingress-nginx/ingress-nginx \
    --namespace ingress-basic \
    --set controller.replicaCount=2 \
    --set controller.nodeSelector."beta\.kubernetes\.io/os"=linux \
    --set defaultBackend.nodeSelector."beta\.kubernetes\.io/os"=linux \
    --set controller.admissionWebhooks.patch.nodeSelector."beta\.kubernetes\.io/os"=linux

```
Get nginx external IP using the command:
```
kubectl --namespace ingress-basic get services -o wide -w nginx-ingress-ingress-nginx-controller
```

Add to hosts file:
```
<external_ip> simple-webv1-ingress.com
```

Run WebServer:
```
helm install webv1 simple-webv1 --namespace ingress-basic
```


Access site:
http://simple-webv1-ingress.com/



1

