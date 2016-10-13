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
# Pods can also be inspected via a shell.
kubectl exec prom-node-exporter-442ce \
  --namespace=monitoring -i -t -- sh
```


##### Updating Configmaps

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