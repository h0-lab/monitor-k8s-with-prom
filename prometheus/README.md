## Prometheus

##### Prep work

See [README.md](../README.md).
See [Alert Manager](../alertmanager/README.md) for alerts.

```bash
# Create the service.
kubectl create -f prometheus/prometheus-service.yml \
  --namespace monitoring

# Then, create the config file.
kubectl create configmap prometheus-config \
  --from-file prometheus/config-map \
  --output yaml --dry-run > manifests/prometheus-configmap.yml

kubectl create -f manifests/prometheus-configmap.yml \
  --namespace monitoring

# Verify that we created the config map.
kubectl get configmaps prometheus-config \
  --output yaml \
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

# Open prometheus.
minikube service prometheus \
  --namespace monitoring
```

##### Updating the Configmap

```
# Recreate the configmap.
# Waiting for https://github.com/kubernetes/kubernetes/pull/33335
# to be merged.
kubectl create configmap prometheus-config \
  --from-file prometheus/config-map/prometheus.yml \
  --namespace monitoring

# Pods will need to be killed to pick up the changes.
# Issue tracking this: https://github.com/kubernetes/kubernetes/issues/22368
```
