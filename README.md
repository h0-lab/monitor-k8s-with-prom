## Experiments with Prometheus on Kubernetes

##### Deploy Prometheus

```bash
# First, create the config file.
kubectl create configmap prometheus-config --from-file prometheus/config-map/prometheus.yml

# Verify that we created the config map.
kubectl get configmaps prometheus-config -o yaml

# Create the deployment.
kubectl create -f prometheus/prometheus-deployment.yml

# Create the service.
kubectl create -f prometheus/prometheus-service.yml
```

##### Deploy Service Loadbalancer

```bash
# Inspect and find the `minikube` node.
kubectl get nodes

# Ensure our node has the correct label.
kubectl label node minikube role=loadbalancer

# Create the haproxy deployment.
kubectl create -f ingress/haproxy-deployment.yml

# Open prometheus.
open $(minikube ip):9090
```
