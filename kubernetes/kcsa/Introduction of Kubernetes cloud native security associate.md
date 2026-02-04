
this is the security measures that needs to be taken while handling the Kubernetes environment.

### thinks to keep in check.
1. no insecure port needs to be open on host level 
2. set up firewall for blocking the access of insecure port.
3. use namespaces for resource isolation.
4. use network policies for pod to pod communication and restrict them.
5. restrict the container image from unauthorized registries. 
6. sign container images for extra layer of security.
7. use tools like trivy or container repository inbuild functionality for image scanning.



