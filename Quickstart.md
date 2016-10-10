
```bash
# Start minikube.
minikube start

# First, create the monitoring namespaces.
kubectl create -f monitoring-namespace.yml

# Create the manifests directory.
mkdir -p manifests/

###
# Alertmanager
###

# Create the service.
kubectl create -f alertmanager/alertmanager-service.yml \
  --namespace monitoring

# Then, create the config file.
kubectl create configmap alertmanager-config \
  --from-file alertmanager/config-map/config.yml \
  --output yaml --dry-run > manifests/alertmanager-configmap.yml

kubectl create -f manifests/alertmanager-configmap.yml \
  --namespace monitoring

# Create the deployment.
kubectl create -f alertmanager/alertmanager-deployment.yml \
  --namespace monitoring

###
# Prometheus
###

# Create the service.
kubectl create -f prometheus/prometheus-service.yml \
  --namespace monitoring

# Then, create the config file.
kubectl create configmap prometheus-config \
  --from-file prometheus/config-map \
  --output yaml --dry-run > manifests/prometheus-configmap.yml

kubectl create -f manifests/prometheus-configmap.yml \
  --namespace monitoring

# Create the deployment.
kubectl create -f prometheus/prometheus-deployment.yml \
  --namespace monitoring

## Consul

# Create the service.
kubectl create -f consul/consul-service.yml \
  --namespace monitoring

# Create the petset.
kubectl create -f consul/consul-petset.yml \
  --namespace monitoring
```
