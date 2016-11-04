## Kube State Metrics

##### Prep work

See [README.md](../README.md).
See [Prometheus README.md](../prometheus/README.md).

```bash
# Create the service.
kubectl create -f kube-state-metrics/kube-metrics-service.yml \
  --namespace monitoring
```

##### Deploy

```bash
# Create the Deployment.
kubectl create -f kube-state-metrics/kube-metrics-deployment.yml \
  --namespace monitoring

# Check the Deployment.
kubectl get pods \
  --namespace monitoring

# Open.
minikube service node-exporter \
  --namespace monitoring
```
