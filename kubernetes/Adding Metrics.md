# Adding Metrics to a Kubernetes Cluster for Pod and Node Resource Monitoring

Monitoring CPU and memory usage of pods and nodes is essential for keeping your Kubernetes cluster **healthy** and performant.
Without metrics, you are effectively running the cluster blind and cannot troubleshoot performance issues or scale workloads properly.

---
## Why do we need metrics in a Kubernetes cluster?

Resource metrics help you:
- See which pods and nodes are consuming the most CPU and memory.
- Detect performance bottlenecks and noisy neighbors early.
- Make informed scaling decisions for Horizontal/Vertical Pod Autoscalers.​
- Troubleshoot issues like OOMKills, throttling, and node pressure.

By default, many Kubernetes clusters do not ship with the Metrics Server installed.
You can verify this by checking for the `metrics-server` pod in the `kube-system` namespace:

```bash
kubectl get pods -n kube-system | grep metrics-server
```

If you do not see a `metrics-server` pod, it means metrics are not yet available in your cluster.

The Metrics Server is a cluster-wide aggregator that collects CPU and memory usage from kubelets on each node and exposes them through the Kubernetes Metrics API, which is what `kubectl top node` and `kubectl top pod` use under the hood.

---
## Exploring the `kubectl top` command

Before installing anything, check what `kubectl top` can do using the help flag:

```bash
kubectl top --help
```

Once Metrics Server is running, you can use:

```bash
# Show node-level resource usage 
kubectl top nodes 
# Show pod-level resource usage in the current namespace 
kubectl top pods
```

If Metrics Server is not installed or not working, you will see an error similar to:

```bash
Error from server (ServiceUnavailable): the server is currently unable to handle the request (get nodes.metrics.k8s.io)
```

This indicates that the `metrics.k8s.io` API is not available in your cluster.​

---
## Installing Metrics Server in the Kubernetes cluster

Metrics Server can be installed by applying the official `components.yaml` manifest.​

Run the following command:

```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

This creates the `metrics-server` deployment (and related resources) in the `kube-system` namespace.

You can then check the logs of the Metrics Server deployment:

```bash
kubectl logs -n kube-system deployment/metrics-server
```

If everything is working correctly, you should see logs indicating successful scraping of metrics from kubelet.

---
## Troubleshooting: Metrics Server pod not Ready

Sometimes the `metrics-server` pod may stay in `CrashLoopBackOff` or `NotReady` state.  
A common reason is that Metrics Server cannot establish a secure TLS connection to kubelet on the nodes, often due to certificate or hostname issues.

You have two broad options:

1. Fix the certificates (secure, recommended for production).
2. Relax TLS verification using `--kubelet-insecure-tls` (acceptable in labs, not recommended for production).

## Option 1: Regenerate certificates securely (recommended)

If you are using a kubeadm-based cluster, you can regenerate control-plane certificates using `kubeadm init phase` commands, Check this link for better configuration [kubelet-serving-certs](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-certs/#kubelet-serving-certs).

1. Regenerate certificates (adjust the config path as per your environment):

```bash
sudo kubeadm init phase certs all --config /path/to/your/configuration/file.yaml
```

2. Restart kubelet on each control-plane and worker node:

```bash
sudo systemctl restart kubelet
```
After this, wait a few moments and re-check the Metrics Server pod status:

```bash
kubectl get pods -n kube-system | grep metrics-server
```

If the TLS setup is correct, the pod should move to `Running` and `Ready`.

## Option 2: Use insecure TLS for Metrics Server (not recommended for production)

For development, lab, or non-critical clusters, you might decide to bypass strict TLS verification by adding the `--kubelet-insecure-tls` flag to the Metrics Server container arguments.

1. Edit the Metrics Server deployment:
```bash
kubectl edit deployment metrics-server -n kube-system
```

2. Under `spec.template.spec.containers[0].args`, add:
```text
spec:   
  template:    
    spec:      
      containers:      
      - name: metrics-server        
        args:        
        - --kubelet-insecure-tls`
```
Save and exit the editor.  
Kubernetes will restart the pod with the updated arguments.

Again, verify that the pod becomes Ready:

```bash
kubectl get pods -n kube-system | grep metrics-server
```

> Note: Using `--kubelet-insecure-tls` disables certificate validation between Metrics Server and kubelet and can expose you to TLS man-in-the-middle attacks, so avoid this in production environments.

---

## Verifying pod and node utilization with `kubectl top`

Once the Metrics Server pod is healthy and Ready, you can start querying live metrics.

Check node-level usage:

```bash
kubectl top nodes
```
Example output:

```text
NAME           CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%
worker-node1   120m         6%     800Mi           40%
worker-node2   90m          4%     700Mi           35%
```

Check pod-level usage in the current namespace:

```bash
kubectl top pods
```

You can also view metrics across all namespaces:

```bash
kubectl top pods -A
```
This gives you a quick, CLI-based view of which workloads are consuming the most resources, and is often the first step in investigating scaling or performance issues.

---
## Reference
- Official `kubectl top` command documentation.[[kubernetes](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_top/)]​