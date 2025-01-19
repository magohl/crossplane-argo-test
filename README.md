# crossplane-argo-test
crossplane-argo-test


kind create cluster --name kind2 --config kind/kind.yaml
kubectl apply -k argocd/install
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
kubectl port-forward -n argocd service/argocd-server 8443:443