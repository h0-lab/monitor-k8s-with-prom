## Kube State Metrics

##### Prep work

See [README.md](../README.md).
See [Prometheus README.md](../prometheus/README.md).

```bash
# Create the service.
kubectl apply -f kube-state-metrics/kube-metrics-service.yml \
  --namespace monitoring
```

##### Deploy

```bash
# Create the Deployment.
kubectl apply -f kube-state-metrics/kube-metrics-deployment.yml \
  --namespace monitoring

# Check the Deployment.
kubectl get pods \
  --namespace monitoring

# Open.
minikube service kube-state-metrics \
  --namespace monitoring
```
