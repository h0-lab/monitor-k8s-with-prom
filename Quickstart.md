##### Getting Started

```bash
# Start minikube.
minikube start

# First, create the monitoring namespaces.
kubectl create -f monitoring-namespace.yml

# Create all services.
find . -iname '*-service.yml' -exec \
  kubectl apply -f {} --namespace=monitoring \;

# Create the manifests directory.
mkdir -p manifests/

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

# Create all pods.
find . -iname '*-pod.yml' -exec \
  kubectl apply -f {} --namespace=monitoring \;

# Create all replication controllers.
find . -iname '*-replicationcontroller.yml' -exec \
  kubectl apply -f {} --namespace=monitoring \;

# Create all daemonsets.
find . -iname '*-daemonset.yml' -exec \
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

# Open.
minikube dashboard

# Delete the cluster when done.
minikube delete
```

##### Cleaning up

```bash
kubectl delete jobs,petsets,deployments,daemonsets,replicationcontrollers,pods,configmaps,secrets,services,thirdpartyresources \
  --namespace monitoring \
  --all

# Delete the cluster when done.
minikube delete
```
