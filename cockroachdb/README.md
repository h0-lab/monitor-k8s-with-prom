## Cockroachdb

##### Prep work

See [README.md](../README.md).
See [Prometheus README.md](../prometheus/README.md).

```bash
# Create the service.
kubectl create -f cockroachdb/cockroachdb-service.yml \
  --namespace monitoring
```

##### Deploy

```bash
# Create the petset.
kubectl create -f cockroachdb/cockroachdb-petset.yml \
  --namespace monitoring

# Check the petset.
kubectl get pods \
  --namespace monitoring

# Open.
minikube service cockroachdb \
  --namespace monitoring
```
