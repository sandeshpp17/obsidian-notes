# Adding a Metrics to the kubernetes cluster for pod and nodes resource monitoring 

## why the metrics is needed in the kubernetes cluster?
--> It need for monitoring pods and nodes resource utilization for better performance of kubernetes cluster. It also needed to find out which pod or node is consuming more resources.

1. Generally the metrics are not added in the k8s cluster.
2. Verify that by checking the pod in kube-system namespace the pod should be present by the name of metrics-server.
3. its used for collecting metrics such as CPU and memory usage from the nodes and pods in your cluster, which `kubectl top node` and `kubectl top pod` commands rely on.

## find more about the kubectl top command using help option

```
kubectl top --help
```
### if the metrics server pod is not present in cluster you will get below error after performing top command.

```
kubectl top nodes
```

![[Pasted image 20240809162942.png]]

# How to add metrics server in kubernetes cluster.

## run to install metric server in kube-system  
--> kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml  

to view to logs of metrics pod

```
kubectl logs -n kube-system deployment/metrics-server
```

## If the metrics pod is not in ready state which means the pod is not connecting with kubelet service if can be happened  due the certificate issue

### To resolve the issue with secure way you can regenerate the certificate of cluster from [[kubeadm init phase]] command.
1. renew certificate 
```
kubeadm init phase certs all --config /path/to/your/configuration/file.yaml
```
2.  restart kubelet service
```
sudo systemctl restart kubelet
```
### resolve issue with pod insecure configuration.
1. Edit the deploy for changing the pod setting  
```
kubectl edit deployment metrics-server -n kube-system  
```
2.  Add the insecure-tls in containers args for passing command.  

```
spec:
  containers:
  - name: metrics-server
   args:
   - --kubelet-insecure-tls
```

## Now check the pods and node utilization.

```
kubectl top nodes
```
![[Pasted image 20240809173230.png]]

reference: https://kubernetes.io/docs/reference/kubectl/generated/kubectl_top/