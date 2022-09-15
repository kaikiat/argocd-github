## Install flask application
1. kubectl create ns demo
2. helm install flask-app .argocd-repositories/flask-app --namespace demo

## Install argocd 
1. Install argocd `brew install argocd`
2. Create argocd namespace `kubectl create namespace argocd`
3. Apply manifests files `kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`
4. Port-forward argocd-server using `kubectl port-forward svc/argocd-server -n argocd 8080:443` in another terminal tab.
5. Login through the UI. Password can be obtained from `kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo`, the username is `admin`.
6. Login via cli using `argocd login localhost:8080 --username admin --password $(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d)`
7. Add github ssh key. Refer to github docs if ssh key has not be generated, otherwise run `argocd repo add git@gitlab.myteksi.net:itn.kaikiat.poh/argocd-demo.git --ssh-private-key-path ~/.ssh/id_rsa`. This can be intepreted as `argocd repo add GITHUB_SSH_URL  --ssh-private-key-path /path/to/ssh/key`, this command with add a github repository to argocd.
8. Verify using `argocd repo list`
9. Apply the manifests file using `kubectl apply -f application.yaml`
