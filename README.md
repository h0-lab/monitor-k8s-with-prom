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