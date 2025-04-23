# Gitlab CD with FLUX-CD

1. use below command to install the flux
    ```bash
    curl -s https://fluxcd.io/install.sh | sudo bash
    ```
2. create personal access token from gitlab and bootstrap the fluxcd using flux command 
    ```bash
    flux bootstrap gitlab --hostname=gitlab360.enlight.dev --owner=enlight360containers --repository=k8s-fluxcd-poc --branch=main --path=./cluster/manifests --deploy-token-auth
    ```

3. check all pods are created
    ```bash
    k -n flux-system get po
    ```

4. install the gitlab cli using below command
    ```bash
    wget https://gitlab.com/gitlab-org/cli/-/releases/v1.55.0/downloads/glab_1.55.0_linux_amd64.tar.gz
    ls
    tar xvf glab_1.55.0_linux_amd64.tar.gz
    cp glab /usr/bin/
    glab version
    ```

5. authenticate your user with glab auth command
    ```bash
    glab auth login --hostname gitlab360.enlight.dev
    ```
6. clone the flux repo to local system 
    ```bash
    git clone https://gitlab360.enlight.dev/enlight360containers/k8s-fluxcd-poc.git
    ```
7. go to file where flux-system is present
    ```bash
    cd k8s-fluxcd-poc/
    ```
8. bootstrap the agent using glab 
    ```bash
    glab cluster agent bootstrap --manifest-path cluster/manifests flux
    ```
9. integration with flux application repo below is command to create nginx test deploy.
    ```bash
    k create deployment ngnix-flux-test --image=nginx:alpine --replicas=3 --dry-run=client -oyaml
    ```
10. create the deploy secret of repo that can be used by flux
    ```bash
    flux create secret git flux-deploy-authentication --url=https://gitlab360.enlight.dev/enlight360containers/nginx-fluxtest --namespace=default --username=gitlab+deploy-token-33 --password=gldt-BWvqSz5ysSxR9Ts1gTrh
    ```

11. check secret
    ```bash
    k -n default get secrets flux-deploy-authentication -o yaml
    ```
12. add git-repository and Kustomization for automated cd add this file in k8s-fluxcd-poc repo in path /cluster/manifests
    gitrepository: nginx-fluxtest.yaml 
    ```yaml
    apiVersion: source.toolkit.fluxcd.io/v1
    kind: GitRepository
    metadata:
      name: nginx-fluxtest-manifests
      namespace: default
    spec:
      interval: 1m0s
      url: https://gitlab360.enlight.dev/enlight360containers/nginx-fluxtest
      ref:
        branch: main
      secretRef:
          name: flux-deploy-authentication
    ```
    Kustomization: 
    ```yaml
    apiVersion: kustomize.toolkit.fluxcd.io/v1
    kind: Kustomization
    metadata:
      name: nginx-fluxtest-kustomization
      namespace: default
    spec:
      interval: 1m
      targetNamespace: default
      sourceRef:
        kind: GitRepository
        name: nginx-fluxtest-manifests
      path: ./
      prune: true
        ```


referance: 
1. flux cd: https://fluxcd.io/flux/components/kustomize/kustomizations/
2. gitlab intergration with flux: https://docs.gitlab.com/user/clusters/agent/getting_started/

video: 
1. https://www.youtube.com/watch?v=EjPVRM-N_PQ&list=PLOi2fMEt2b0hsf-FAo9rJ5Orwe9lC6nlq
2. https://www.youtube.com/watch?v=JmER6QzCv5s