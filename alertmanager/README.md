## Alertmanager

##### Prep work

See [README.md](../README.md).

```bash
# Create the service.
kubectl create -f alertmanager/alertmanager-service.yml \
  --namespace monitoring

# Then, create the config file.
kubectl create configmap alertmanager-config \
  --from-file alertmanager/config-map/config.yml \
  --output yaml --dry-run > manifests/alertmanager-configmap.yml

kubectl create -f manifests/alertmanager-configmap.yml \
  --namespace monitoring

# Verify that we created the config map.
kubectl get configmaps alertmanager-config \
  --output yaml \
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
