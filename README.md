# gitops-example-159
gitops-example-159-image-updater

# gitops-example-158
gitops-example-158


Commands to run:
minikube start --driver=docker
kubectl get nodes

helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
helm search repo argocd

helm show values argo/argocd-image-updater --version 1.0.1 > argocd-image-updater.yaml

Run terraform commands here and then run the following commands 

helm status argocd -n argocd
helm list --pending -A

helm list -A
kubectl get pods -n argocd
kubectl get secret -n argocd

kubectl get secrets argocd-initial-admin-secret -o yaml -n argocd
echo "bGFWeEwtcTZEUnFTS2RYMg==" | base64 -d | laVxL-q6DRqSKdX2
kubectl port-forward svc/argocd-server -n argocd 8080:80

username: admin
password from above

Next is setting up public repo and public image 

Now in 1-example is where we deploy using argocd and give reference to application
Once you have the application.yaml file run the kubectl command'
Before applying we need to have the docker images and login setup:
docker login -u <username> -p <password> or docker login -u <username> and enter 
And next is pulling the necessary image and tagging for testing purpose for that go through the public or private repo

kubectl apply -f 1-example/application.yaml

You need to apply maunally in argocd application 
Click on sync it will work automatically from now on 

And to automate this process of tagging the image to the infra repo is done through a small example of upgrade.sh
And make it executable 

When using 3-example we are not gonna use https and specify the private repo use ssh instead which a secure way of connecting 

So first we need to create an ssh key using this command:
ssh-keygen -t ed25519 -f ~/.ssh/argocd_ed25519
or ssh-keygen -t rsa -b 4096 -f ~/.ssh/argocd_ed25519

Then upload the public key to github repo under setting and deploy key
And next is create a seceret in kubernetes using file in 3-example
Then run 
kubectl apply -f 3-example/git-repo-secret.yaml
Then apply application:
kubectl apply -f 3-example/application.yaml

But still it wont be able to pull the images as it is in private repo:
So create a read only token in dockerhub and store it here 
And then use it in the kubectl create secret command 

kubectl create secret docker-registry dockerconfigjson -n foo \
    --docker-server="https://index.docker.io/v1/" \
    --docker-username=howaboutwepullsomeimages \
    --docker-password=<PAT> 


Next running helm chart command to deploy the application in argocd 
helm repo add metrics-server https://kubernetes-sigs.github.io/metrics-server/
helm search repo metrics-server

next run this: kubectl apply -f 4-example/application.yaml
And then to check if it working run these commands:
kubectl top pods -n kube-system -> You will see a different output
kubectl top nodes -> Same here 


- name: ARGOCD_APPLICATIONS_API
  value: "true"

- name: ENABLE_LEGACY_APPLICATIONS_API
  value: "true"

- name: ARGOCD_IMAGE_UPDATER_ENABLE_CRD
  value: "false"
