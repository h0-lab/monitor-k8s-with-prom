### Some example queries

##### The state of the cluster.

# How much memory is the prometheus container using in the monitoring namespace?
container_memory_usage_bytes{container_name="prometheus",namespace="monitoring"}

# Sum up the memory usage in the monitoring namespace by pod.
sum by(pod_name) (container_memory_usage_bytes{namespace="monitoring"})

# Sum up by prometheus job container memory usage for monitoring namespace for all pods that contain the name "prometheus".
sum by(job) (container_memory_usage_bytes{namespace="monitoring", pod_name=~"prometheus.*"})

# Inspect how much memory is being used by a certain image
container_memory_usage_bytes{namespace="default",image=~"datadog/docker-dd-agent:.*"}

##### We can also do some detective / troubleshooting work as well.

# When was this image last seen running?
container_last_seen{image="prom/node-exporter:master"}

# Give the top 3 images that use the most memory.
topk(2, sum(container_memory_usage_bytes{image!=""}) by (image))

# How many bytes of the filesystem were consumed per docker container?
sum(container_fs_usage_bytes{name!=""}) by (name)

##### We can also query information about the kubernetes server itself.

# What is the request count for the Kubernetes API server?
sum(rate(apiserver_request_count[1m]))

##### We can also query information about nodes as well.

# How many cores are available?
machine_cpu_cores{job="kubernetes-nodes"}

# How much memoyr is available?
machine_memory_bytes{job="kubernetes-nodes"}
