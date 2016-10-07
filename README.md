## Experiments with Prometheus on Kubernetes

##### Deploying Prometheus

```bash
# First, create the config file.
kubectl create configmap prometheus-config --from-file prometheus/config-map/prometheus.yml

# Verify that we created the config map.
kubectl get configmaps prometheus-config -o yaml

# Create the deployment.
kubectl create -f prometheus/prometheus-deployment.yml
```
