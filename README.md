# Kubernetes-learning

# DAY 1
Introduction
Why & What ?
Benefits of Kubernetes
Compare with other container orchestrator engine
minikube intoduction & setup

# DAY 2

# DAY 3

## How to run

### pod.yml
make sure minikube is running -> if not run "minikube start"
then run **"kubectl apply -f pod.yml"**
to check status **"kubectl get po welcom-pod"**
to get detailed info **"kubectl describe po welcome-pod"**
to delete the pod **"kubectl delete po welcome-pod"**

# initcontainer-nodeapp.yml
kubectl apply -f initcontainer-nodeapp.yml

kubectl get po foss-app-with-init

kubectl describe po foss-app-with-init

kubectl delete -f initcontainer-nodeapp.yml


