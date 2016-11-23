## Grafana

##### Prep work

See [README.md](../README.md).
See [Prometheus README.md](../prometheus/README.md).

```bash
# Create the service.
kubectl create -f grafana/grafana-service.yml \
  --namespace monitoring

# Then, create the config file.
kubectl create configmap grafana-config \
  --from-file grafana/config-map \
  --output yaml --dry-run > manifests/grafana-configmap.yml

kubectl create -f manifests/grafana-configmap.yml \
  --namespace monitoring

# Verify that we created the config map.
kubectl get configmaps grafana-import-dashboards \
  --output yaml \
  --namespace monitoring
```

##### Deploy

```bash
# Create the deployment.
kubectl create -f grafana/grafana-deployment.yml \
  --namespace monitoring

# Check the deployment.
kubectl get pods \
  --namespace monitoring

# Create the job.
kubectl create -f grafana/grafana-import-job.yml \
  --namespace monitoring

# View.
kubectl get pods \
  -l app=grafana,kind=ui -o template \
  --template="{{range.items}}{{.metadata.name}}{{end}}" \
  --namespace monitoring \
  | xargs -I{} kubectl port-forward {} --namespace monitoring 3000
```
