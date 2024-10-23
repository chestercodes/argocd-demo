# argocd-demo


## setup cluster

create cluster 

``` bash
k3d cluster create --config ./k3d/config.yaml --kubeconfig-update-default --kubeconfig-switch-context --wait
```

wait ~30 seconds, open k9s to see rest waking up

``` bash
k9s -A
```

## install sample app

``` bash
kubectl apply -f sample/manifest.yaml
start microsoft-edge:http://dotnet-sample-127-0-0-1.nip.io/
```

## install argocd

``` bash
helm dependency update charts/argo-cd
kubectl create namespace argocd
helm install argocd charts/argo-cd --namespace argocd
# wait about 90s
start microsoft-edge:http://argocd-127-0-0-1.nip.io/
# login is admin/hiargo
```

## install argocd

``` bash
kubectl apply -f argocd.yaml
```

## spin up app-of-apps

``` bash
kubectl apply -f app-of-apps.yaml
```


## tear down

Need to run this **after** the session has happened.

``` bash
k3d cluster delete argocd-demo
```