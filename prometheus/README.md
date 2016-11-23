## Prometheus

##### Prep work

See [README.md](../README.md).
See [Alert Manager](../alertmanager/README.md) for alerts.

```bash
# Create the service.
kubectl apply -f prometheus/prometheus-service.yml \
  --namespace monitoring

# Create the configmap.
kubectl apply -f prometheus/prometheus-configmap.yml \
  --namespace monitoring
```

##### Deploy

```bash
# Create the deployment.
kubectl apply -f prometheus/prometheus-deployment.yml \
  --namespace monitoring

# Check the deployment.
kubectl get pods \
  --namespace monitoring

# View.
kubectl get pods \
  -l app=prometheus -o template \
  --template="{{range.items}}{{.metadata.name}}{{end}}" \
  --namespace monitoring \
  | xargs -I{} kubectl port-forward {} --namespace monitoring 9090
```
