1. Install ArgoCD in k8s cluster
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

2. Configure ArgoCD with "Application" CRD
# get the base64 password:
kubectl get secret argocd-initial-admin-secret -n argocd -o yaml

# decode it (bash)
echo RkhuNkcyZVpvMkNsbzdLUg== | base64 --decode # AE3IvwghyC8yCBoS

# configure your application.yaml
(example in this folder)
 
# apply changes
kubectl apply -f application.yaml

# port-fowarding for accessing the ui
kubectl port-forward svc/argocd-server -n argocd 8080:443

3. Test our setup by updating Deployment.yaml