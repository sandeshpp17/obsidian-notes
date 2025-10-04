### 1. Virtual Networks

**Virtual Networks** provide a logical networking layer that allows pods to communicate as if they are on the same physical network, regardless of the underlying infrastructure.

- **Pod IPs**: Each pod gets a unique IP address from a predefined subnet, allowing for direct communication.
- **CNI Plugins**: The Container Network Interface (CNI) plugins (like Calico, Flannel, or Weave) create virtual networks, handling IP address allocation and routing.

### 2. Bridges

**Bridges** are used to connect different network segments, allowing communication between them.

- **Linux Bridge**: When a pod is created, the CNI plugin can create a Linux bridge on the node. This bridge acts like a virtual switch, allowing packets to be routed between pods and the host network.
    
- **Bridge Functionality**: Each pod gets a virtual Ethernet interface connected to the bridge, allowing it to send and receive packets through the bridge. The bridge forwards traffic between the pod interfaces and the node's network interface.
    

### Communication Flow

1. **Pod Creation**: When a pod is scheduled, the CNI plugin creates a virtual network interface for the pod and connects it to the bridge.
    
2. **IP Assignment**: The pod is assigned an IP address from the virtual network managed by the CNI.
    
3. **Traffic Flow**:
    
    - **Same Node**: If a node wants to communicate with a pod on the same node, it sends packets directly to the pod's IP. The bridge forwards the packets to the appropriate pod interface.
    - **Different Node**: For pods on different nodes, the traffic may be encapsulated by the CNI (in the case of overlay networks) and sent to the destination node, where it is decapsulated and forwarded to the appropriate pod through the bridge.
4. **Routing**: The Kubernetes networking model ensures that all nodes can route packets to any pod, leveraging the CNI plugin's routing capabilities.

# To check the bridde ip of the node
```
ip a
```

```
tunl0@NONE: <NOARP,UP,LOWER_UP> mtu 1480 qdisc noqueue state UNKNOWN group default qlen 1000
    link/ipip 0.0.0.0 brd 0.0.0.0
    inet 192.168.12.0/32 scope global tunl0
       valid_lft forever preferred_lft forever

```
In the last line you will find the tunl0 which indicate virtual bridge of the node.

### Summary

In summary, virtual networks and bridges in Kubernetes enable seamless communication between nodes and pods by providing a flexible and scalable networking model. The use of CNI plugins, bridges, and IP assignment mechanisms allows for efficient traffic management, supporting diverse applications running within the cluster.