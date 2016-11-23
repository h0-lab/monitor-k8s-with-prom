## Weave

##### Prep work

See [README.md](../README.md).

```bash
# Create the service.
kubectl apply -f weave/weavescope-service.yml \
  --namespace monitoring
```

##### Deploy

```bash
# Create the daemonset.
kubectl apply -f weave/weavescope-daemonset.yml \
  --namespace monitoring

# Create the deployment.
kubectl apply -f weave/weavescope-deployment.yml \
  --namespace monitoring

# Check the deployment.
kubectl get pods \
  --namespace monitoring

# Open.
minikube service weave \
  --namespace monitoring
```
