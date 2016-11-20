## Alertmanager

##### Prep work

See [README.md](../README.md).

```bash
# Create the service.
kubectl create -f alertmanager/alertmanager-service.yml \
  --namespace monitoring

# Create the configmap.
kubectl create -f alertmanager/alertmanager-configmap.yml \
  --namespace monitoring
```

##### Deploy

```bash
# Create the deployment.
kubectl create -f alertmanager/alertmanager-deployment.yml \
  --namespace monitoring

# Check the deployment.
kubectl get pods \
  --namespace monitoring

# Open.
minikube service alertmanager \
  --namespace monitoring
```
