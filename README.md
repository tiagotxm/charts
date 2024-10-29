# Kind
kind create cluster --config kind.yaml

# ArgoCD

```
kubectl create namespace argocd

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl port-forward svc/argocd-server -n argocd 8080:443
```
- Recuperar a senha para login

````
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
````
ou via CLI

```
argocd admin initial-password -n argocd

```
- Instalar o Argo CLI:
`brew install argocd`

- Se o repo for privado(SSH):
https://argo-cd.readthedocs.io/en/stable/user-guide/private-repositories/#ssh-private-key-credential

export ARGOCD_OPTS='--port-forward-namespace argocd'

argocd login localhost:8080 --insecure

argocd repo add git@github.com:tiagotxm/k8s-labs.git --ssh-private-key-path ~/.ssh/d9xs-argocd

helm repo add spark-operator https://kubeflow.github.io/spark-operator

helm repo update

helm pull spark-operator/spark-operator --untar

kubectl create namespace spark-jobs