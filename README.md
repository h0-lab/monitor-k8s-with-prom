## Experiments with Prometheus on Kubernetes

##### Some prep work

```bash
# Start minikube.
minikube start

# First, create the monitoring namespaces.
kubectl create -f prometheus/monitoring-namespace.yml

# Then, create the config file.
kubectl create configmap prometheus-config \
  --from-file prometheus/config-map/prometheus.yml \
  --output yaml --dry-run > manifests/prometheus-configmap.yml

kubectl create -f manifests/prometheus-configmap.yml \
  --namespace monitoring

# Verify that we created the config map.
kubectl get configmaps prometheus-config \
  --output yaml \
  --namespace monitoring

# Create the service.
kubectl create -f prometheus/prometheus-service.yml \
  --namespace monitoring
```

##### Deploy Prometheus

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

##### Deploy the Node Exporter

```bash
# Next, create the node exporter.
kubectl create -f prometheus/prometheus-node-exporter.yml \
  --namespace monitoring

# Open prometheus.
minikube service prom-node-exporter \
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

##### Debugging

```bash
# Pods can also be inspected via a shell.
kubectl exec prom-node-exporter-442ce \
  --namespace=monitoring -i -t -- sh
```

## Experiments with Grafana on Kubernetes

##### Some prep work

```bash
# Then, create the config file.
kubectl create configmap grafana-import-dashboards \
  --from-file grafana/config-map \
  --output yaml --dry-run > manifests/grafana-import-dashboards-configmap.yml

kubectl create -f manifests/grafana-import-dashboards-configmap.yml \
  --namespace monitoring

# Verify that we created the config map.
kubectl get configmaps grafana-import-dashboards \
  --output yaml \
  --namespace monitoring

# Create the service.
kubectl create -f grafana/grafana-service.yml \
  --namespace monitoring
```

##### Deploy Grafana

```bash
# Create the deployment.
kubectl create -f grafana/grafana-deployment.yml \
  --namespace monitoring

# Check the deployment.
kubectl get pods \
  --namespace monitoring

# Create the deployment.
kubectl create -f grafana/grafana-import-job.yml \
  --namespace monitoring

# Open prometheus.
minikube service grafana \
  --namespace monitoring
```
