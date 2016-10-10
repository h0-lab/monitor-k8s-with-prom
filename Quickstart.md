
```bash
# Start minikube.
minikube start

# First, create the monitoring namespaces.
kubectl create -f monitoring-namespace.yml

# Create the manifests directory.
mkdir -p manifests/

# Create all services.
find . -iname '*-service.yml' -exec \
  kubectl apply -f {} --namespace=monitoring \;

configmaps=(
  alertmanager
  consul
  grafana
  prometheus
)

for i in "${configmaps[@]}"; do
  echo "Creating $i configmap"
  kubectl create configmap "$i-config" \
    --from-file "$i/config-map" \
    --output yaml --dry-run > "manifests/$i-configmap.yml"
done;

# Create all config maps.
find . -iname '*-configmap.yml' -exec \
  kubectl apply -f {} --namespace=monitoring \;

# Create all daemonsets.
find . -iname '*-ds.yml' -exec \
  kubectl apply -f {} --namespace=monitoring \;

# Create all deployments.
find . -iname '*-deployment.yml' -exec \
  kubectl apply -f {} --namespace=monitoring \;

# Create all petsets.
find . -iname '*-petset.yml' -exec \
  kubectl apply -f {} --namespace=monitoring \;

# Run all jobs.
find . -iname '*-job.yml' -exec \
  kubectl apply -f {} --namespace=monitoring \;

# Open dashboard.
minikube dashboard

# Delete the cluster when done.
minikube delete
```
