## Prometheus

##### Prep work

See [README.md](../README.md).
See [Alert Manager](../alertmanager/README.md) for alerts.

```bash
# Create the service.
kubectl create -f prometheus/prometheus-service.yml \
  --namespace monitoring

# Create the configmap.
kubectl create -f prometheus/prometheus-configmap.yml \
  --namespace monitoring
```

##### Deploy

```bash
# Create the deployment.
kubectl create -f prometheus/prometheus-deployment.yml \
  --namespace monitoring

# Check the deployment.
kubectl get pods \
  --namespace monitoring

# Open.
minikube service prometheus \
  --namespace monitoring
```
