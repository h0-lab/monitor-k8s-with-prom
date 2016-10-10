## Consul

##### Prep work

See [README.md](../README.md).
See [Prometheus README.md](../prometheus/README.md).

```bash
# Create the service.
kubectl create -f consul/consul-service.yml \
  --namespace monitoring

# Then, create the config file.
kubectl create configmap consul-config \
  --from-file consul/config-map \
  --output yaml --dry-run > manifests/consul-configmap.yml

kubectl create -f manifests/consul-configmap.yml \
  --namespace monitoring

# Verify that we created the config map.
kubectl get configmaps consul-config \
  --output yaml \
  --namespace monitoring
```

##### Deploy

```bash
# Create the petset.
kubectl create -f consul/consul-petset.yml \
  --namespace monitoring

# Check the petset.
kubectl get pods \
  --namespace monitoring

# Open.
minikube service consul \
  --namespace monitoring
```
