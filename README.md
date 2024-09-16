# DevOps-CD
The repo includes argoCd - Flux setup and usage


# Setup minikube
* 
```bash
    minikube start --nodes 2 --driver=docker
```

# install argoCD

* 
```bash
    kubectl create namespace argocd
    kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

    kubectl port-forward svc/argocd-server -n argocd 8080:443

    kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode; echo

```

## argoCD Usage

* 

# install flux

* 
```bash
    brew install fluxcd/tap/flux
```

* 
```bash
    curl -s https://fluxcd.io/install.sh | sudo bash
```

```bash
    flux install
```


## Flux Usage
### source
*  
```bash 
flux create source git my-repo \
  --url=https://github.com/my-org/my-repo \
  --branch=main \
  --interval=1m
```

### kustomize
* 
```bash
flux create kustomization my-app \
  --source=GitRepository/my-repo \
  --path=./path/to/kustomization \
  --prune=true \
  --interval=10m
```
### bootstrap
* 
```bash
flux bootstrap github \
  --owner=my-org \
  --repository=my-repo \
  --branch=main \
  --path=clusters/my-cluster
```
###
