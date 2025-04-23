# Deny internal namespace communication and allow external node communication

## External communication
In the kubernetes the communication between pod and node works through the virtual bridge network which is provided by the CNI and CRI.
The virtual bridge is created for pod to node communication.
more at [[Network relation between pod and node]]

## Pod to pod Namespace communication

Pod communicate with pod directly with the help of CNI plugins where are kube-proxy works as router for routing traffic of pods. 
more at [[Cross namespace networking of pod]]

## Namespace network isolation using network policy

If we apply the network policy to restrict the namespace network isolation it also blocks the external communication some times we need the external communication to access individual pod by adding the tunl0 ip CIDR in the network policy can allow the external communication of pod.

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: Namespace-pod-isolation
  namespace: <Namespace>
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector: {}
    - ipBlock:
        cidr: 192.168.12.0/32
    - ipBlock:
        cidr: 192.168.111.64/32
    - ipBlock:
        cidr:  192.168.28.64/32
    ports:
    - protocol: TCP
      port: 80
    - protocol: TCP
      port: 443
```


more at:
[Network policy for K8s](https://kubernetes.io/docs/concepts/services-networking/network-policies/#networkpolicy-resource)
[node and pod networking](https://medium.com/google-cloud/understanding-kubernetes-networking-pods-7117dd28727)