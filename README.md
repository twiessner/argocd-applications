
# Introduction
This repository contains a small, simple collection of ArgoCD applications to initialize a vanilla Kubernetes cluster.

# Usage
My example setup is based on MacOS and Minikube.

## Install ArgoCD CLI

```bash
brew install argocd
```

## Create ArgoCD App of App

```bash
# Forward the local ArgoCD service
kubectl port-forward svc/argocd-server -n argocd 8080:443

# Login to ArgoCD
argocd login localhost:8080

# Create the master app of app
argocd app create bootstrap \
    --dest-namespace argocd \
    --dest-server https://kubernetes.default.svc \
    --repo https://github.com/twiessner/argocd-applications.git \
    --path bootstrap
    --directory-recurse

# Sync the created app, to install all childs    
argocd app sync bootstrap
```

You can open a browser an type `localhost:8080` to open the ArgoCD Web UI.