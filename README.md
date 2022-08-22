# gitops-argocd
cf. https://atmarkit.itmedia.co.jp/ait/articles/2107/30/news018.html

# setup
## argocd cli
```
brew tap argoproj/tap
brew install argoproj/tap/argocd
```

## argocd install
```
helm repo add argo https://argoproj.github.io/argo-helm
helm install argo-cd --namespace argocd --create-namespace argo/argo-cd --version 3.6.11
helm list -n argocd
kubectl get pods -n argocd
```

## port forward
```
kubectl port-forward service/argo-cd-argocd-server -n argocd 8080:443
```

## login
### generate passowrd
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo
```

### create account
```
argocd login localhost:8080
username: admin
passowrd: <above-password>
```

## ArgoCD add repo
```
argocd repo add https://github.com/mida-hub/gitops-argocd.git --username <user_name> --password <access_token>

argocd repo list
```

## uninstall
```
helm uninstall argo-cd -n argocd
```

# ArgoCD Create App
## create app
```
kubectl apply -f application_dev.yaml
```

## port forward
```
kubectl port-forward service/wordpress -n dev 30000:80
```

## delete app
```
kubectl delete -f application_dev.yaml
```
