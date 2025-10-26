# FlatlineOps

**What**: ArgoCD Configuration repository. It will utilize the a **App-of-Apps** pattern.

**Purpose**: for my home-lab kubernetes clusters.
Just playing and deving around.

**Repo Name**: Tribute to Dixie Flatline, the dead cowboy whose construct lives on. A console cowboy who operates with ghostlike precision 👻

## Install
Kubectl Apply argocd `01-install.yaml` file:
```sh
❯ kubectl apply -n argocd -f 01-install.yaml
```

There after to access the ArgoCD Web UI.

Step 1. Get the admin password:
```sh
❯ kubectl get secrets -n argocd argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```
Or with argocd cli:
```sh
❯ argocd admin initial-password -n argocd
```

Step 2. Port-forward to localhost the ArgoCD server with kubectl port-forword:
```
❯ kubectl port-forward -n argocd service/argocd-server 8080:80
```

The login with the username of `admin` and the password copied from the kubernetes secret `argocd-initial-admin-secret`.

### Admin Change Password
Following best practices from [ArgoCD documentation](https://argo-cd.readthedocs.io/en/stable/getting_started/) is to change the admin password and then delete the `argocd-initial-admin-secret`. The secret serves no other purpose than to store the initially generated password in clear and can safely be deleted at any time. It will be re-created on demand by Argo CD if a new admin password must be re-generated.

Using the knowledge from the step 1 of the getting access to ArgoCD Web UI:
```sh
❯ argocd login <ARGOCD_SERVER>
```
Then to update the password run:
```sh
❯ argocd account update-password
```
After the new password is set delete the `argocd-initial-admin-secret` with kubectl:
```sh
❯ kubectl delete secrets -n argocd argocd-initial-admin-secret
```
