# setup kubernetes cluster.

## kubeadm phases

allow you to control the phases of kubernetes cluster setup. skipping the phases of cluster and initialize certain phase again.

You can also use `--help` to see the list of sub-phases for a certain parent phase:

```
sudo kubeadm init phase control-plane --help
```

`kubeadm init` also exposes a flag called `--skip-phases` that can be used to skip certain phases.

```
sudo kubeadm init --skip-phases=control-plane,etcd --config=configfile.yaml
```
## setup kubernetes cluster using kubeadm command 

```
kubeadm init 
```
when you initialize the cluster using the kubeadm command it setup the cluster automatically.
by adding static pod configuring the network security and certificate and many more.

to add configuration to kuberentes cluster the config is give.
## Two ways to give the configuration initiation
1. using `--<configurations>`
2. by the config file `--config /path/to/your/kubeadm-config.yaml`
3. config file look like below.
```
apiVersion: kubeadm.k8s.io/v1beta2
kind: ClusterConfiguration
kubernetesVersion: v1.24.0
apiServer:
  certSANs:
    - "192.168.1.100" # IP address of the master node
    - "k8s-master.example.com" # DNS name of the master node
    - "10.96.0.1" # Cluster IP of the Kubernetes API Server
controlPlaneEndpoint: "k8s-master.example.com:6443" # Control plane endpoint
networking:
  podSubnet: "10.244.0.0/16" # The pod network CIDR
  serviceSubnet: "10.96.0.0/12" # The service network CIDR
etcd:
  local:
    dataDir: /var/lib/etcd
```

reference: https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-init/