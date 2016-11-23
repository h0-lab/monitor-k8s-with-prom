## Experiments with Prometheus on Kubernetes

##### Prep work

```bash
# Start minikube.
minikube start

# First, create the monitoring namespaces.
kubectl create -f monitoring-namespace.yml

# Create the manifests directory.
mkdir -p manifests/
```

##### Debugging

```bash
# Have minikube be extra verbose.
minikube start \
  --vm-driver virtualbox \
  --v=10 \
  --show-libmachine-logs \
  --alsologtostderr

# Open the ui.
kubectl proxy &
open http://localhost:8001/ui

# Exec a shell
kubectl get pods \
  -l app=dd-agent -o template \
  --template="{{range.items}}{{.metadata.name}}{{end}}" \
  --namespace monitoring \
  | xargs -I{} kubectl exec {} --namespace monitoring -i -t -- sh

# Port Forwarding
kubectl get pods \
  -l app=prometheus -o template \
  --template="{{range.items}}{{.metadata.name}}{{end}}" \
  --namespace monitoring \
  | xargs -I{} kubectl port-forward {} --namespace monitoring 9090
```

##### Updating Configmaps

```
# Then, create the config file.
kubectl create configmap grafana-config \
  --from-file grafana/config-map \
  --output yaml --dry-run > manifests/grafana-configmap.yml

kubectl create -f manifests/grafana-import-dashboards-configmap.yml \
  --namespace monitoring

# Recreate the configmap.
# Waiting for https://github.com/kubernetes/kubernetes/pull/33335
# to be merged.
kubectl create configmap prometheus-config \
  --from-file prometheus/config-map/prometheus.yml \
  --namespace monitoring

# Pods will need to be killed to pick up the changes.
# Issue tracking this: https://github.com/kubernetes/kubernetes/issues/22368
```

##### Cleaning up

```bash
kubectl delete jobs,petsets,deployments,daemonsets,replicationcontrollers,replicasets,pods,configmaps,secrets,services,thirdpartyresources \
  --namespace monitoring \
  --all
```
