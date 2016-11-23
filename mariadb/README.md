## Mariadb

##### Prep work

See [README.md](../README.md).
See [Prometheus README.md](../prometheus/README.md).

```bash
# Create the service.
kubectl apply -f mariadb/mariadb-service.yml \
  --namespace monitoring
```

##### Deploy

```bash
# Create the deployment.
kubectl apply -f mariadb/mariadb-deployment.yml \
  --namespace monitoring

# Check the deployment.
kubectl get pods \
  --namespace monitoring

# Open.
minikube service mariadb \
  --namespace monitoring
```
