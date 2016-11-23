## Fluentd to Elasticsearch

##### Prep work

See [README.md](../README.md).

```bash
# Create the services.

kubectl apply -f fluentd-elasticsearch/kibana-service.yml \
  --namespace monitoring

kubectl apply -f fluentd-elasticsearch/es-service.yml \
  --namespace monitoring
```

##### Deploy

```bash
# Create the pods.

kubectl apply -f fluentd-elasticsearch/es-controller.yml \
  --namespace monitoring

kubectl apply -f fluentd-elasticsearch/kibana-controller.yml \
  --namespace monitoring

kubectl apply -f fluentd-elasticsearch/fluentd-daemonset.yml \
  --namespace monitoring

# View.
kubectl get pods \
  -l app=kibana -o template \
  --template="{{range.items}}{{.metadata.name}}{{end}}" \
  --namespace monitoring \
  | xargs -I{} kubectl port-forward {} --namespace monitoring 5601

kubectl get pods \
  -l app=elasticsearch -o template \
  --template="{{range.items}}{{.metadata.name}}{{end}}" \
  --namespace monitoring \
  | xargs -I{} kubectl port-forward {} --namespace monitoring 9108
```
