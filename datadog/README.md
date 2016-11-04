## Datadog

##### Prep work

See [README.md](../README.md).

Base64 encode the secret.

```bash
echo -n {Secret} | base64
```

Replace it in `EncodedSecret`.

```yml
kind: Secret
apiVersion: v1
metadata:
  name: datadog
data:
  api-key: {EncodedSecret}
```

Add your datadog key as a secret.

```bash
kubectl create -f datadog/.secrets/datadog-key-secret.yml \
  --namespace monitoring
```

##### Deploy

```bash
# Create the DaemonSet.
kubectl create -f datadog/datadog-daemonset.yml \
  --namespace monitoring

# Check the DaemonSet.
kubectl get pods \
  --namespace monitoring
```