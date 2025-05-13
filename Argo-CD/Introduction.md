There are multiple CD tool in the market which can be used for continuous deployment. Like, gitlab CICD and Jenkins.

Argo-cd is used for continuous deployment reducing manual efforts.

### why to use argocd.
we can use cd with jenkins but there are some challenges to use it.
- install and setup tools, like kubectl
- configure access to k8s
- configure access to cloud platform
- security challenges
- No visibility of deployment status

### workflow
1. agrocd uses pull based mechanism where the agent is installed in the argocd and its connect to git repository. 
2. agrocd agent looks for changes in the git repo and if its found some changes that it will be applied in the kubernetes cluster.

`Test` --> `Build Image` --> `Push To Docker Repo` --> `Update k8s Manifest File`

3. keep the git repository of app source code and app configuration separate to simplify thing only see the changes in manifest file.
4. supported file, YAML,HELM CHART, Kustomize and template of yaml.

### Single source of truth
ArgoCD works on actual state and desired state of kubernetes cluster.
- when anything change on the git repo it tried to change same in k8s cluster.
- if someone tries to change anything in the cluster it revert back the changes and applies manifest in git repo.
- ArgoCD watches the changes in the cluster as well.
- it compares desired state in git repo with its actual state in the k8s cluster.

### Disaster recovery
when the manifest of applications are manages within the code-base and some disaster happens at CSP level. by using the argoCD we can replicate whole setup as it is in another region.


### K8s management via git.

-  you don't need to create the role and rolebinding in k8s cluster to grant access for other user. its can be managed at git level and once changes are done you can approve it to merge in deployment branch. 
- ArgoCD uses the ETCD database of k8s cluster for updates of manifest. it creates the visibility of k8s cluster ArgoCD.
- 