## Consul

##### Prep work

See [README.md](../README.md).
See [Prometheus README.md](../prometheus/README.md).

```bash
# Create the service.
kubectl apply -f consul/consul-service.yml \
  --namespace monitoring

# Create the configmap.
kubectl apply -f consul/consul-configmap.yml \
  --namespace monitoring
```

##### Deploy

```bash
# Create the petset.
kubectl apply -f consul/consul-petset.yml \
  --namespace monitoring

# Check the petset.
kubectl get pods \
  --namespace monitoring

# Open.
minikube service consul \
  --namespace monitoring
```
