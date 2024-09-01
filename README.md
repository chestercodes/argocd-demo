# argocd-demo

## setup cluster

create cluster 

``` bash
k3d cluster create --config ./k3d/config.yaml --kubeconfig-update-default --kubeconfig-switch-context --wait
```

wait ~60 seconds

see what has been created

``` bash
kubectl get all -A
```

## install argocd

``` bash
cd charts/argo-cd
helm dependency update .
kubectl create namespace argocd
helm install argocd . --values ./values.yaml --namespace argocd
# kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

## install apps

``` bash
# cd charts/argo-cd
cd resources
kubectl apply -f project.yaml
helm install argocd . --values ./values.yaml --namespace argocd
# kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

