# CNAmsterdam2023
1. Create a Firewall rule to open the firewall to access your cluster

2. Set the project and region:
```
gcloud config set compute/zone us-central1-a
gcloud config set project cs-nonprod
```

3. Create your cluster:
```
gcloud container clusters create kcd-colombia --num-nodes=1 --tags=allin,allout --machine-type=n1-standard-2 --no-enable-network-policy
```

4. Install ArgoCD:
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

5. Install ArgoCD CLI:
```
brew install argocd
```

6. Access ArgoCD installation:
```
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Open http://localhost:8080 in your browser

7. Get the current password in a terminal
```
argocd admin initial-password -n argocd
```

8. Update the password using the UI

9. Create namespace for your Kubernetes deployments:
```
kubectl create namespace development 
```

10. Create your ArgoCD Projects and Apps of Apps:
```
kubectl apply -f projects/
```

11. Create your apps using the Github Action Called "Create App" in the URL https://github.com/sergioarmgpl/CNAmsterdam2023/actions

12. Find your project and see how the application are created.

13. Check for the new services created for the apps
```
kubectl get svc -n development
```

14. Check for the new deployments created for the apps
```
kubectl get deploy -n development
```

15. Access an application
```
kubectl port-forward svc/APPNAME-srv 5001:5000 -n development
```
