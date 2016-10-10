## Node exporter

##### Prep work

See [README.md](../README.md).
See [Prometheus README.md](../prometheus/README.md).

```bash
# Create the service.
kubectl create -f node-exporter/node-exporter-service.yml \
  --namespace monitoring
```

##### Deploy

```bash
# Create the DaemonSet.
kubectl create -f node-exporter/node-exporter-ds.yml \
  --namespace monitoring

# Check the DaemonSet.
kubectl get pods \
  --namespace monitoring

# Open.
minikube service node-exporter \
  --namespace monitoring
```
