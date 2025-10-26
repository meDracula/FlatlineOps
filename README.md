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

Step 2. Port-forward to localhost the ArgoCD server with kubectl port-forword:
```
❯ kubectl port-forward -n argocd service/argocd-server 8080:80
```

The login with the username of `admin` and the password copied from the kubernetes secret `argocd-initial-admin-secret`.
