ArgoCD can be installed as CRD in k8s cluster. below is the command to install it.

```bash
kubectl create namespace argocd 
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

To integrate the k8s cluster with git we can use multiple method.

1. via CLI
First we need to set the current namespace to argocd running the following command:

`kubectl config set-context --current --namespace=argocd`

Create the example guestbook application with the following command:

```bash
argocd app create guestbook --repo https://github.com/argoproj/argocd-example-apps.git --path guestbook --dest-server https://kubernetes.default.svc --dest-namespace default
```

2. Creating Apps Via UI[¶](https://argo-cd.readthedocs.io/en/stable/getting_started/#creating-apps-via-ui "Permanent link")

Open a browser to the Argo CD external UI, and login by visiting the IP/hostname in a browser and use the credentials set in step 4 or locally as explained in [Try Argo CD Locally](https://argo-cd.readthedocs.io/en/stable/try_argo_cd_locally/).

After logging in, click the **+ New App** button as shown below:

![+ new app button](https://argo-cd.readthedocs.io/en/stable/assets/new-app.png)

Give your app the name `guestbook`, use the project `default`, and leave the sync policy as `Manual`:

![app information](https://argo-cd.readthedocs.io/en/stable/assets/app-ui-information.png)

Connect the [https://github.com/argoproj/argocd-example-apps.git](https://github.com/argoproj/argocd-example-apps.git) repo to Argo CD by setting repository url to the github repo url, leave revision as `HEAD`, and set the path to `guestbook`:

![connect repo](https://argo-cd.readthedocs.io/en/stable/assets/connect-repo.png)

For **Destination**, set cluster URL to `https://kubernetes.default.svc` (or `in-cluster` for cluster name) and namespace to `default`:

![destination](https://argo-cd.readthedocs.io/en/stable/assets/destination.png)

After filling out the information above, click **Create** at the top of the UI to create the `guestbook` application:

![destination](https://argo-cd.readthedocs.io/en/stable/assets/create-app.png)