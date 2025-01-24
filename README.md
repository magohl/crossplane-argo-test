# crossplane-argo-test

curl sS https://webi.sh/k9s | sh && source ~/.config/envman/PATH.env

minikube start

kubectl apply -k argocd/install

kubectl wait --for=condition=ready pod -l app.kubernetes.io/name=argocd-server --namespace argocd --timeout=300s

kubectl apply -n argocd -f argocd/crossplane-bootstrap/crossplane-helm-secret.yaml

kubectl apply -n argocd -f argocd/crossplane-bootstrap/crossplane.yaml

kubectl apply -n argocd -f argocd/crossplane-bootstrap/crossplane.yaml

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

kubectl port-forward -n argocd service/argocd-server 8443:443