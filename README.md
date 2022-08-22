# gitops-argocd
cf. https://atmarkit.itmedia.co.jp/ait/articles/2107/30/news018.html

# setup
## argocd cli
```
brew tap argoproj/tap
brew install argoproj/tap/argocd
```

## argocd deploy
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
### passowrd の生成
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo
```

### アカウント作成
```
argocd login localhost:8080
username: admin
passowrd: uJYgOSTkVLgdfdPx
```

## ArgoCD リポジトリ登録
```
argocd repo add https://github.com/mida-hub/gitops-argocd.git --username mida-hub --password <access_token>

argocd repo list
```

# ArgoCD Create App
create app on browser

## port forward
```
kubectl port-forward service/wordpress -n dev 30000:80
```
