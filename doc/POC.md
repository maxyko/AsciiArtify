# ArgoCD

## Prerequisites
- Having locally deployed K8s cluster. In our case ***k3d*** tool can be used for running local K8s(k3s) cluster:
[k3d demo](https://github.com/maxyko/AsciiArtify/blob/main/doc/Concept.md#%D0%B4%D0%B5%D0%BC%D0%BE%D0%BD%D1%81%D1%82%D1%80%D0%B0%D1%86%D1%96%D1%8F)
- Create a cluster:
  ```
  k3d cluster create argo
  ```
  Check cluster context:
  ```
  kubectl config current-context
  ```

## To install ArgoCD in your K8s cluster:

- #### Create a namespace for ArgoCD:
```
kubectl create namespace argocd
```

- #### Apply ArgoCD manifest:
```
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

- ### Check that everything up and running:
```
kubectl get all -n argocd
```
```
kubectl get po -n argocd -w
```


## To get access to ArgoCD Web UI:

- ### Use ***port-forward*** to forward local ports to ArgoCD svc/pod:
```
kubectl port-forward svc/argocd-server -n argocd 8080:443 &
```

- ### Get a password of ***admin*** user of ArgoCD Web UI:
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```
Secure way to get the password in a clipboard using ***pbcopy*** utility:
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d | pbcopy
```

- ### Use a web browser to get ArgoCD Web UI:
***Url*** (accept using of a self-signed certificate):
```
https://127.0.0.1:8080
```
Username/Password:
```
Username: admin
Password: <get_passwd_see_above>
```
