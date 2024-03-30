## Interacting with k3s cluster.

As k3s includes `kubectl` tool, we can use this to interact with the cluster.
```bash
kubectl get nodes -o wide
kubectl get pods -A
kubectl get svc -A
kubectl get deployment -A
```

### Deploy nginx application using kubectl.
```bash
# Create a nginx application.
kubectl create deployment nginx-deployed-using-kubectl --image=nginx
kubectl get deployment
kubectl expose deployment nginx-deployed-using-kubectl --type=NodePort --port=80
kubectl get pods -A

# Check forwarded port.
kubectl get svc -A

# Use the above port to access the application.
curl -v http://IP_ADDR_OF_K3S_CLUSTER:PORT_FROM_ABOVE
```

### Deploy nginx application using helm.
Helm tool default uses [Artifact Hub](https://artifacthub.io/) repository.
```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install nginx-deployed-using-helm bitnami/nginx
kubectl get deployment
kubectl get pods -A

# Check forwarded port.
kubectl get svc -A

# Use the above port to access the application.
curl -v http://IP_ADDR_OF_K3S_CLUSTER:PORT_FROM_ABOVE
```
