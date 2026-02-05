
in Kubernetes cluster there are multiple components that communicates with each other. 
each component has the insecure communication. it essential the make those component talk with each other in secure way by configuring them with [[TLS certificate]].

1. kube-api server
2. schedular
3. controller manager
4. etcd 
5. kubelet

above are the k8s components that needs to communicate with each other securely. 

